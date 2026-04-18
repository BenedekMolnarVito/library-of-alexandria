---
title: "Gemma 4 on vLLM vs Ollama: Benchmarks on a 96 GB Blackwell GPU"
source: "https://allenkuo.medium.com/gemma-4-on-vllm-vs-ollama-benchmarks-on-a-96-gb-blackwell-gpu-804ca4845a21"
author:
  - "[[Allen Kuo (kwyshell)]]"
published: 2026-04-08
created: 2026-04-18
description: "Gemma 4 on vLLM vs Ollama: Benchmarks on a 96 GB Blackwell GPU Update (2026–04–17): The BF16-vs-Q4_K_M comparison in this article has a known precision asymmetry — we flagged it in “Lessons …"
tags:
  - "clippings"
---
> *Update* *(2026–04–17): The* *BF16-vs-Q4\_K\_M* *comparison* *in* *this* *article* *has* *a* *known* *precision* *asymmetry* *— we* *flagged* *it* *in* *“Lessons* *Learned* *#2”* *but* *deferred* *the* *full* *NVFP4* *comparison.*
> 
> *That* *follow-up* *is* *now* *published:* [Finishing What We Started: Gemma 4 NVFP4 on vLLM, Desktop Blackwell, WSL2](https://allenkuo.medium.com/finishing-what-we-started-gemma-4-nvfp4-on-vllm-desktop-blackwell-wsl2-b2088c34815a)
> 
> *— covers* *the* *8-layer* *install* *chain,* *the* *fair* *apples-to-apples* *benchmarks,* *and* *a* *nuanced* *engine* *comparison.* *The* *benchmarks* *below* *remain* *valid* *as* *the* *“vLLM* *running* *out* *of* *the* *box”* *baseline.*

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*uhRHOf18mYjZQaCbCHr9vQ.png)

Google’s Gemma 4 family just dropped — E4B (8B), 26B MoE, and 31B Dense — and I benchmarked all three on both vLLM and Ollama using the same RTX PRO 6000 Blackwell workstation. The results tell a clear story about when each engine shines.

**TL;DR:** vLLM wins TTFT (3x faster) and concurrent throughput (3x higher). Ollama wins single-user decode speed (1.5x faster). The 26B MoE model is the surprise MVP — faster than the smaller E4B on vLLM, with 26B-class intelligence at 4B-class speed.

## Test Setup

**Hardware:** NVIDIA RTX PRO 6000 Blackwell Workstation Edition (97,887 MiB VRAM, 400W power limit)

**Software:**

- vLLM 0.19.1rc1 on WSL2 Ubuntu 24.04 (BF16 precision, CUDA graphs enabled)
- Ollama latest stable on Windows 11 native (Q4\_K\_M quantization)
- Same prompt for both: *“Summarize what uvx and nvitop are in 4 concise bullet points.”*
- `max_tokens=256`, `temperature=0`, 3 warm runs each

**Key difference:** vLLM runs models in BF16 (16-bit, full precision). Ollama uses Q4\_K\_M (4-bit quantized via GGUF). This is not the same-weight comparison — it reflects what each engine actually uses by default.

## Getting Gemma 4 Running

## Ollama (Windows native) — one command

```c
ollama run gemma4:26b
```

Ollama auto-downloads the Q4\_K\_M GGUF. No setup required.

## vLLM (WSL2) — requires upgrades

Gemma 4 uses the `gemma4` architecture, which requires `vLLM >= 0.19` (stable release supports it) **and** `transformers >= 5.5.0`. The catch: vLLM 0.19 pins `transformers <= 4.57.6`, which does **not** recognize Gemma 4. You must upgrade transformers separately. Without it, you get:

```c
The checkpoint you are trying to load has model type \`gemma4\`
but Transformers does not recognize this architecture.
```

**Upgrade steps:**

```c
# In your WSL2 vLLM venv
source ~/.venvs/vllm/bin/activate
export PATH="$HOME/.local/bin:$PATH"
cd /tmp  # avoid importing local vllm source tree
```
```c
# 1. Install or upgrade to vLLM >= 0.19
# Option A: stable release
uv pip install -U vllm
# Option B: nightly (for Blackwell / bleeding-edge)
uv pip install -U --pre vllm --extra-index-url https://wheels.vllm.ai/nightly# 2. Upgrade transformers (required — vLLM does not auto-pull >= 5.x)
uv pip install --upgrade transformers# 3. Verify
python -c "import transformers; print(transformers.__version__)"
# Must be >= 5.5.0
python -c "import vllm; print(vllm.__version__)"
# Must be >= 0.19
```

**Note:** There is a [known issue](https://github.com/vllm-project/vllm/issues/38887) where Gemma 4 E4B runs at only ~9 tok/s on RTX 4090 due to forced TRITON\_ATTN fallback. On Blackwell (SM 12.x), I observed 124 tok/s — suggesting the issue is GPU-generation-specific. If you hit unusually slow performance, check if a newer vLLM nightly or Triton version resolves it.

**Download models (BF16 safetensors from HuggingFace):**

```c
export HF_HOME=/path/to/cache
python -c "
from huggingface_hub import snapshot_download
snapshot_download('google/gemma-4-E4B-it', local_dir='/path/to/models/gemma-4-E4B-it')
snapshot_download('google/gemma-4-26B-A4B-it', local_dir='/path/to/models/gemma-4-26B-A4B-it')
snapshot_download('google/gemma-4-31B-it', local_dir='/path/to/models/gemma-4-31B-it')
"
```

Model sizes on disk: E4B ~15 GiB, 26B ~49 GiB, 31B ~59 GiB.

**Launch vLLM:**

```c
cd /tmp  # important: avoid local source tree shadowing installed package
source ~/.venvs/vllm/bin/activate
export VLLM_NO_USAGE_STATS=1
```
```c
vllm serve /path/to/models/gemma-4-26B-A4B-it \
  --port 8000 \
  --tensor-parallel-size 1 \
  --max-model-len 32768 \
  --gpu-memory-utilization 0.80 \
  --language-model-only
```

Notes:

- `--language-model-only` skips vision/audio encoders (text-only benchmark)
- `--gpu-memory-utilization 0.80` leaves 20% VRAM for the OS and other apps — never use the default 0.90 on a desktop workstation (I learned this the hard way — see my [first article](https://allenkuo.medium.com/vllm-or-ollama-on-blackwell-benchmarks-landmines-and-what-agents-actually-need-5dc539bb28ef))
- First startup takes 2–5 minutes for `torch.compile` and CUDA graph capture (102 graphs). Subsequent starts use the compiled cache and are faster.
- Gemma 4 uses heterogeneous head dimensions (`head_dim=256, global_head_dim=512`), which forces the TRITON\_ATTN backend automatically.

## The Numbers

## Decode Speed (tokens/second, single request)

Ollama wins decode across all three models. This is the “how fast does text appear” metric.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Tnu4fPc7pyqG6ddJLuB7vQ.png)

- **E4B** — Ollama 196 tok/s vs vLLM 124 tok/s (Ollama 1.6x faster)
- **26B** — Ollama 181 tok/s vs vLLM 131 tok/s (Ollama 1.4x faster)
- **31B** — Ollama 58 tok/s vs vLLM 22 tok/s (Ollama 2.6x faster)

The gap widens with model size. For the 31B Dense model, BF16 weights are 59 GiB — the GPU spends most of its time moving data through the memory bus. Ollama’s Q4\_K\_M cuts that to ~18 GiB, giving it a massive bandwidth advantage.

## Time to First Token (TTFT)

vLLM wins TTFT across the board. This is the “how long before the first character appears” metric.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*a18fSl8aO8k_jejn46w86A.png)

- **E4B** — vLLM 58ms vs Ollama 184ms (vLLM 3.2x faster)
- **26B** — vLLM 68ms vs Ollama 194ms (vLLM 2.9x faster)
- **31B** — vLLM 92ms vs Ollama 201ms (vLLM 2.2x faster)

58ms is imperceptible to humans. 184ms is a noticeable pause. In agent loops where TTFT is multiplied by 10–20 steps, this adds up to seconds of difference.

## Concurrent Throughput (4 parallel requests)

This is where vLLM’s architecture truly differentiates. Continuous Batching lets multiple requests share the same GPU batch.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*7TZ0BlYkIwLzzLtPcsJZ_g.png)

- **E4B** — vLLM 441 tok/s vs Ollama 124 tok/s (vLLM 3.6x higher)
- **26B** — vLLM 316 tok/s vs Ollama 124 tok/s (vLLM 2.5x higher)
- **31B** — vLLM 93 tok/s vs Ollama 58 tok/s (vLLM 1.6x higher)

Ollama processes requests sequentially — one finishes before the next starts. vLLM interleaves them. At 4 concurrent users, vLLM delivers up to 3.6x total throughput.

## VRAM Usage

This is Ollama’s strongest advantage for desktop users.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*WlOkm1a7z9tzmAs6FZV0zA.png)

- **E4B** — Ollama 29 GiB vs vLLM 89 GiB
- **26B** — Ollama 51 GiB vs vLLM 90 GiB
- **31B** — Ollama 83 GiB vs vLLM 90 GiB

vLLM pre-allocates a KV cache pool at startup, consuming a fixed ~90 GiB regardless of model size (with `--gpu-memory-utilization 0.80`). Ollama only uses what the model needs. On a desktop where you also run ComfyUI, games, or other GPU apps, Ollama leaves room. vLLM monopolizes.

## The Surprise: 26B MoE is Faster Than E4B on vLLM

This was the most unexpected result. The 26B model — which has 26 billion parameters — decoded at **131 tok/s** on vLLM, faster than the 8B E4B at 124 tok/s.

The reason is architecture. Gemma 4 26B is a **Mixture of Experts (MoE)** model. It has 26B total parameters but only activates ~4B per token. The active parameter count determines compute and memory bandwidth requirements, not the total count.

On Ollama, the same pattern holds: 26B runs at 181 tok/s vs E4B at 196 tok/s — closer, but 26B is still remarkably fast for a model 3x larger. The slight slowdown is due to the larger weight file needing more memory bandwidth for expert routing.

The practical implication: **26B MoE gives you 26B-class intelligence at near-4B speed.** It correctly identified `uvx` as a Python tool runner (E4B hallucinated it as a GPU monitoring tool), while running only 5% slower on vLLM and 8% slower on Ollama.

## The 31B Problem: When BF16 Hurts

The 31B Dense model exposes vLLM’s weakness on desktop hardware. At 22 tok/s decode, it is painfully slow — slower than Ollama’s 58 tok/s by 2.6x.

The root cause is simple arithmetic. 31B in BF16 means ~59 GiB of weights. Each decode step reads the entire weight matrix. On the RTX PRO 6000’s 1.8 TB/s GDDR7 bus:

- BF16: 59 GiB / 1.8 TB/s = 33ms per token → ~30 tok/s theoretical max
- Q4\_K\_M: ~18 GiB / 1.8 TB/s = 10ms per token → ~100 tok/s theoretical max

vLLM’s 22 tok/s is actually close to the BF16 theoretical limit. Ollama’s 58 tok/s benefits from 4-bit quantization cutting the memory traffic by 3.3x.

For models above ~20B parameters on a single GPU, quantization is not optional — it is the difference between usable and unusable. vLLM would need AWQ/GPTQ quantized weights to compete here.

## When to Use What

**Choose vLLM + Gemma 4 26B MoE when:**

- Building agent systems (low TTFT + fast prefill + concurrent multi-agent)
- Serving multiple users via API
- Running RAG pipelines with long context
- Quality matters more than raw typing speed

**Choose Ollama + Gemma 4 26B when:**

- Single-user interactive chat (181 tok/s feels instant)
- Desktop coexistence with ComfyUI, games, other GPU apps
- Quick experimentation (one command setup)
- VRAM is limited (51 GiB vs 90 GiB)

**Choose Ollama + Gemma 4 E4B when:**

- Maximum decode speed needed (196 tok/s)
- Minimal VRAM footprint (29 GiB)
- Tasks where hallucination on niche topics is acceptable

**Avoid Gemma 4 31B on vLLM BF16** unless you have quantized weights. At 22 tok/s, it is not competitive. Use Ollama for 31B (58 tok/s with Q4\_K\_M) or wait for AWQ/GPTQ variants.

## How This Compares to My Qwen3.5 Results

I previously benchmarked Qwen3.5–9B on the same hardware. The patterns are consistent:

- **vLLM wins TTFT and concurrency** across both model families
- **Ollama wins single-user decode** across both model families
- **The decode gap narrows** when comparing similar parameter counts (Qwen3.5–9B: 1.5x, Gemma 4 E4B: 1.6x)
- **Quantization advantage grows with model size** (E4B 1.6x → 31B 2.6x)

The Gemma 4 26B MoE result is unique — no equivalent in the Qwen3.5 test. MoE architecture is a genuine win for inference efficiency, giving larger-model intelligence at smaller-model cost.

## Lessons Learned

**1\. MoE models are the sweet spot for local inference.** Gemma 4 26B delivers the best quality-per-VRAM-dollar. Its 131 tok/s on vLLM and 181 tok/s on Ollama make it practical for daily use.

**2\. BF16 vs Q4\_K\_M is the real differentiator, not the engine.** Most of the decode speed gap between vLLM and Ollama comes from precision, not from engine architecture. If vLLM ran Q4 (via GGUF support or equivalent), the gap would largely close.

**3\. TTFT and concurrency are vLLM’s structural advantages.** These come from PagedAttention and Continuous Batching — architectural features that cannot be replicated by changing quantization. If your workload is TTFT-sensitive (agents, RAG, interactive tools), vLLM wins regardless of precision.

**4\. Desktop VRAM management remains vLLM’s biggest weakness.** Pre-allocating 90 GiB at startup is a server assumption that does not translate to desktop use. This is the core motivation for my native Windows LLM engine project.

> ***Update: Confirmed* *in* *the***  
> [Finishing What We Started: Gemma 4 NVFP4 on vLLM, Desktop Blackwell, WSL2](https://allenkuo.medium.com/finishing-what-we-started-gemma-4-nvfp4-on-vllm-desktop-blackwell-wsl2-b2088c34815a) *— NVFP4* *closes* *most* *of* *the* *BF16* *gap* *(E4B* *decode* *124→149* *tok/s,* *TTFT* *58→17ms)* *but* *Q4\_K\_M* *still* *wins* *single-user* *decode* *by*  
> *24–30%.* *vLLM* *keeps* *its* *TTFT* *and* *concurrency* *advantages* *regardless* *of* *quantization*

## Test Environment

- **GPU:** NVIDIA RTX PRO 6000 Blackwell (97,887 MiB, 400W power limit)
- **Host OS:** Windows 11 Pro
- **vLLM:** 0.19.1rc1 @ WSL2 Ubuntu 24.04, BF16, CUDA graphs, `--gpu-memory-utilization 0.80`
- **Ollama:** Latest stable, Windows native, Q4\_K\_M (GGUF)
- **Models:** google/gemma-4-E4B-it, google/gemma-4–26B-A4B-it, google/gemma-4–31B-it
- **Benchmark date:** 2026–04–08

*This is the second in a series of benchmarks on my path toward a native Windows LLM engine. The first article covered* [*Qwen3.5–9B benchmarks and Blackwell pitfalls*](https://allenkuo.medium.com/vllm-or-ollama-on-blackwell-benchmarks-landmines-and-what-agents-actually-need-5dc539bb28ef)*.*

*Benchmarks conducted with identical prompts, parameters, and hardware. vLLM benchmark script uses streaming SSE with token counting; Ollama benchmark uses native API metrics. Raw data available on request.*[Gemma 4](https://medium.com/tag/gemma-4?source=post_page-----804ca4845a21---------------------------------------)[Vllm](https://medium.com/tag/vllm?source=post_page-----804ca4845a21---------------------------------------)[Ollama](https://medium.com/tag/ollama?source=post_page-----804ca4845a21---------------------------------------)[Nvidia](https://medium.com/tag/nvidia?source=post_page-----804ca4845a21---------------------------------------)[LLM](https://medium.com/tag/llm?source=post_page-----804ca4845a21---------------------------------------)

[![Allen Kuo (kwyshell)](https://miro.medium.com/v2/resize:fill:60:60/0*qFiFRIcfLG-jBnUF.)](https://allenkuo.medium.com/?source=post_page---post_author_info--804ca4845a21---------------------------------------)[166 following](https://allenkuo.medium.com/following?source=post_page---post_author_info--804ca4845a21---------------------------------------)

## Responses (1)

Benedek Molnar

What are your thoughts?

```c
This comparison makes no sense. You should compare vllm and ollama serving the same model quantization. Or even better since ollama is serving a 4 bit quant, serve nvfp4 on vllm to truly take advantage of Blackwell.
```

84

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--804ca4845a21-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)