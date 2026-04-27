---
title: "How I Doubled My Local LLM’s Speed (Without Buying New Hardware)"
source: "https://medium.com/write-a-catalyst/how-i-doubled-my-local-llms-speed-without-buying-new-hardware-0201539eb935"
author:
  - "[[Amar Chetri]]"
  - "[[PhD]]"
published: 2026-02-22
created: 2026-04-23
description: "How I Doubled My Local LLM’s Speed (Without Buying New Hardware) I remember the frustration vividly. I had just downloaded a powerful 70B parameter model, quantized it nicely to Q4_K_M, and fired …"
tags:
  - "clippings"
---
I remember the frustration vividly. I had just downloaded a powerful 70B parameter model, quantized it nicely to Q4\_K\_M, and fired up my inference server. The first response came out… at a crawl. About 8 tokens per second. Watching it generate text felt like waiting for paint to dry. I knew my RTX 3090 was capable of more, but I couldn’t afford to drop thousands on a second GPU just to make chat responses feel snappy.

So I went down the rabbit hole. I spent weeks testing every optimization technique I could find — quantization tweaks, batch size adjustments, thread counts, offloading strategies. And somewhere along the way, I discovered two techniques that completely transformed my local LLM experience: speculative decoding and multi-token prediction.

Today, the same 70B model on the same RTX 3090 runs at over 160 tokens per second. That’s not a typo. I literally doubled — actually more than doubled — my inference speed without spending a dime on new hardware.

Here’s exactly how I did it, step by step.

## Understanding Why Local LLMs Run Slow

Before we dive into solutions, we need to understand the problem. Why do large language models run so slowly on consumer hardware, even when you have a decent GPU?

The bottleneck isn’t computation — it’s memory bandwidth.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*2m9Mi-BG6-usaUiWPrDe2Q.png)

Standard autoregressive generation processes one token at a time, requiring a full forward pass for each new token.

Here’s what’s happening under the hood. When you run an LLM, the model weights (billions of parameters) are stored in your GPU’s VRAM. For every single token the model generates, those weights need to be read from VRAM into the GPU’s compute cores. On a system with 128 GB/s memory bandwidth, a 70B model in 4-bit precision (about 35GB) limits you to roughly 3–4 token reads per second. The math is brutal.

The standard approach — called autoregressive generation — makes this worse. The model generates one token at a time, sequentially. Forward pass for token 1, then forward pass for token 2, then forward pass for token 3. Each pass requires reading those weights again.

This is the fundamental speed limit we’re all fighting against. But here’s the good news: there are ways to cheat this limit.

## Technique #1: Speculative Decoding (The Game Changer)

The first technique I implemented was speculative decoding. And honestly, it sounds too good to be true when you first hear about it.

## How Speculative Decoding Works

Think of it as a collaboration between an experienced manager and a fast intern.

- The large base model (your main LLM) is the manager — knowledgeable but slow, taking time to think through each word.
- The small draft model is the intern — much faster but less accurate, able to type up ideas quickly.

Here’s the workflow that changed everything for me:

1. Instead of the manager writing one word at a time, the intern quickly drafts a short sequence of the next 5–16 words.
2. The manager then looks at this entire draft in a single, parallel step.
3. It verifies each word in the draft simultaneously.
4. As long as the intern’s predictions match what the manager would have written, those words are accepted instantly.
5. The moment the manager finds a word it would have chosen differently, it corrects that single word and discards the rest.
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*N4txuQ1eFZI48r3-87BBYQ.png)

Speculative decoding uses a small draft model to generate token sequences in parallel, verified by the larger target model.

This is faster because instead of doing five sequential forward passes (one per token), you’re doing two passes: one for the draft and one for verification. On memory-bandwidth-bound systems, this can yield massive speedups.

## Real-World Results

In my testing with a Llama-3.3–70B model as the target and Llama-3.2–1B as the draft, I saw throughput jump from around 30 tokens per second to over 160 t/s on my RTX 3090. Other users have reported similar gains — 4x to 5x speed increases are common.

The best part? The output is identical to what the large model would have produced on its own. The large model verifies every accepted token, so there’s no quality loss whatsoever.

## Hardware Requirements

The main catch: you need enough VRAM to load both models simultaneously. Here’s what that looks like in practice:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*XF9P1quQiTa9LcibbPycfg.png)

For my RTX 3090 (24GB VRAM), the 70B + 3B combination actually exceeds VRAM. I had to use a 1B draft model instead, which fit comfortably.

## How I Set It Up in Llama.cpp

Here’s the exact command I use to run speculative decoding with llama.cpp’s server:

bash

```rb
./llama-server \
 -m ./models/Llama-3.3-70B-Instruct-Q4_K_M.gguf \
 -md ./models/Llama-3.2-1B-Instruct-Q4_K_M.gguf \
 -ngl 99 -ngld 99 -fa --port 9999 -c 8192 \
 --draft-max 16 --draft-min 5
```

Let me break down what each flag does:

- `-m`: Path to your main (large) model
- `-md`: Path to your draft (small) model
- `-ngl 99`: Offload all layers of the main model to GPU
- `-ngld 99`: Offload all layers of the draft model to GPU
- `-fa`: Enable flash attention
- `--draft-max 16`: Maximum number of tokens the draft model generates
- `--draft-min 5`: Minimum tokens before verification

## Pro Tip: Multi-GPU Setup

If you have multiple GPUs, place the draft model on a separate, slower GPU to reserve bandwidth on your primary GPU for the main model. Use the `-ngld` flag to control this.

## Technique #2: Multi-Token Prediction (The Next Level)

After I got speculative decoding working, I stumbled on something even more interesting: multi-token prediction (MTP). This is a newer technique that takes the same core idea but eliminates the need for a separate draft model.

## What Makes MTP Different

Multi-token prediction is a form of self-speculative decoding. Instead of using a separate draft model, the main model is trained to predict multiple future tokens at once.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*pEuSwH_2tm3Epc0rVNhCig.png)

Multi-token prediction generates multiple tokens in parallel, dramatically reducing the number of forward passes required.

The process works like this:

1. Speculation Pass: The model processes your prompt and simultaneously generates a block of guesses — say, \[Token 1, Token 2\_guess, Token 3\_guess, Token 4\_guess, Token 5\_guess\].
2. Verification Pass: Instead of checking each guess one by one, the model verifies them all in a single parallel pass. It takes the sequence \[Prompt + Token 1 + Token 2\_guess + …\] as input and calculates the “correct” next token for every position simultaneously.
3. Acceptance: If all guesses are correct, you’ve generated five tokens with just two forward passes — a 2.5x speedup.

## The VRAM Advantage

This is where MTP really shines for hardware-constrained users. Standard speculative decoding requires loading a completely separate draft model, which consumes its own VRAM. With MTP, the main model is trained to be its own draft model. The only overhead comes from tiny prediction “heads” added to the model, often consuming less than 1% additional VRAM.

For me, this was huge. I could get speculative decoding-style speedups without sacrificing the VRAM needed for larger context windows.

## The Catch (And It’s a Big One)

Here’s the honest truth: models must be specifically trained for MTP. You can’t just enable it on any model. The model needs to be fine-tuned with MTP heads to support this feature.

That means our existing library of popular GGUF models — like standard Llama 3 or Mistral — won’t work with MTP out of the box. For the community to benefit, model creators need to release versions with MTP baked in.

## Which Models Support MTP?

A growing number of models are being released with MTP capabilities:

- DeepSeek V3 / R1
- Qwen3-Next
- GLM-4.5

If you’re using vLLM, you can enable MTP with simple command-line flags:

For DeepSeek:

```rb
vllm serve deepseek-ai/DeepSeek-R1 --speculative-config='{"method": "deepseek_mtp", "num_speculative_tokens": 1}'
```

For Qwen3-Next:

```rb
vllm serve Qwen/Qwen3-Next-80B-A3B-Instruct --speculative-config '{"method": "qwen3_next_mtp", "num_speculative_tokens": 2}'
```

Note: llama.cpp doesn’t yet support MTP, though development is active. When I tried loading an MTP model, these layers were skipped. Given the potential performance gains — especially for CPU and hybrid inference — this is one of the most anticipated features for the project.

## Technique #3: Hyperparameter Tuning (The Cherry on Top)

Once I had speculative decoding running, I wanted to squeeze out every last token per second. That’s when I discovered automated hyperparameter tuning.

## Why Hyperparameters Matter

Hyperparameters are the control knobs for your AI model. Adjusting them properly can mean the difference between a model that’s slow and unresponsive versus one that’s snappy and efficient.

Key parameters that impact speed include:

- Batch size: How many tokens processed together
- Thread count: CPU threads for parallel processing
- GPU layer count: How many layers are offloaded to GPU
- Context size: Maximum sequence length

## Automated Optimization with llama-optimus

I found a tool called llama-optimus that completely changed my tuning workflow. It’s a Python tool that automatically optimizes llama.cpp performance flags for maximum throughput using Bayesian optimization.

Here’s how I use it:

```rb
# Install
pip install llama-optimus
```
```rb
# Run optimization
llama-optimus --llama-bin ~/llama.cpp/build/bin --model ~/models/my-model.gguf --trials 25 -r 3 --metric tg
```

The tool does something brilliant:

1. Warms up the system to avoid misleading cold-start results
2. Uses Bayesian optimization (via Optuna) to search for the best parameter combinations
3. Tests different batch sizes, thread counts, and GPU layer counts
4. Outputs ready-to-copy commands for optimal inference

When I ran this on my setup, it discovered a configuration I never would have tried manually:

```rb
Best config: {'batch': 4096, 'flash': 1, 'u_batch': 1024, 'threads': 4, 'gpu_layers': 93}
Best tg tokens/sec: 73.5
```

The optimized command it gave me:

```rb
llama-server --model my_model.gguf -t 4 --batch-size 4096 --ubatch-size 1024 -ngl 93 --flash-attn
```

## The Warm-Up Trick

One thing I learned: cold starts lie to you. When you first load a model, your system caches aren’t warmed up, and you might see artificially high token rates. Llama-optimus includes a warm-up phase to ensure you’re measuring real-world, steady-state performance.

## Putting It All Together: My Complete Optimization Workflow

Here’s the step-by-step process I now use for any new model:

## Step 1: Choose Your Models

- For speculative decoding: Pick a main model and a compatible draft model from the same family (same tokenizer)
- For MTP: Look for models explicitly trained with MTP support (DeepSeek, Qwen3-Next)

## Step 2: Quantize Appropriately

I use Q4\_K\_M for the best balance of speed and quality. For draft models, even smaller quantizations (Q4\_0) work fine.

## Step 3: Run Automated Tuning

```rb
llama-optimus --llama-bin ~/llama.cpp/build/bin --model ~/models/main-model.gguf --trials 30 --metric tg
```

## Step 4: Launch with Speculative Decoding

Take the optimized parameters and add speculative decoding flags:

```rb
./llama-server \
 -m ./models/main-model.gguf \
 -md ./models/draft-model.gguf \
 -t [optimal threads] \
 --batch-size [optimal batch] \
 --ubatch-size [optimal ubatch] \
 -ngl [optimal layers] \
 -ngld 99 \
 --draft-max 16 \
 --draft-min 5 \
 --flash-attn
```

## Step 5: Benchmark and Compare

Always benchmark before and after. I use `llama-bench` to get reliable numbers:

```rb
llama-bench --model my-model.gguf -t 4 -ngl 99 -n 128 -p 128 -r 3
```

## The Results: What 2x Speed Looks Like

Before optimization, my 70B model crawled at 30 tokens/second — usable but not pleasant for chat. After implementing speculative decoding with a 1B draft model and optimizing hyperparameters, I’m consistently getting 160+ tokens/second.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*MITjI-qV8daW0Mg3SxsVfg.png)

Real-world performance gains from speculative decoding on an RTX 3090.

[https://via.placeholder.com/800x400?title=Before+vs+After+Performance](https://via.placeholder.com/800x400?title=Before+vs+After+Performance)

\*Caption: Real-world performance gains from speculative decoding on an RTX 3090.\*

That means:

- A 500-token response takes 3 seconds instead of 16 seconds
- Real-time chat feels instantaneous
- I can run batch processing jobs in a fraction of the time

All on the exact same hardware I’ve had for two years.

## Common Mistakes I Made (So You Don’t Have To)

## Mistake #1: Wrong Model Order

I once swapped the main and draft models. Instead of speedup, I got massive slowdown. Always: large model as `-m`, small model as `-md`.

## Mistake #2: Ignoring Tokenizer Compatibility

Draft models must share the same tokenizer as the main model. That’s why using models from the same family (Llama 3.2 1B with Llama 3.3 70B) works so well.

## Mistake #3: Not Warming Up

Cold starts gave me artificially high numbers that didn’t reflect real performance. Always warm up your system before benchmarking.

## Mistake #4: Overloading VRAM

I tried using a 3B draft model with my 70B main, but together they exceeded my 24GB VRAM. The system started swapping to system RAM, and performance tanked. Stick to smaller draft models if you’re VRAM-constrained.

## What’s Next on My Optimization List

The field is moving fast. Here’s what I’m watching:

## Quantization-Aware Training (QAT)

Google recently released Gemma 3 models with QAT optimization. Unlike traditional quantization (which converts after training), QAT trains models to be resilient to quantization from the start. Early tests show QAT models maintain quality even at 4-bit precision, with virtually no perplexity drop.

## Better MoE Offloading

For mixture-of-experts models like DeepSeek, new techniques allow smarter offloading — keeping “always active” parameters on GPU while routing experts to CPU. The performance gains are dramatic.

## Glinthawk Architecture

Researchers at Microsoft have demonstrated a two-tiered architecture that offloads attention mechanisms to lower-end compute, achieving 5.9x throughput improvements. This is bleeding-edge, but it shows where the field is heading.

## Final Thoughts

You don’t need to buy new hardware to get dramatically better performance from your local LLMs. The techniques I’ve shared — speculative decoding, multi-token prediction, and automated hyperparameter tuning — are pure software optimizations that leverage what you already have more efficiently.

The key takeaways:

1. Speculative decoding can give you 4–5x speedups with compatible model pairs
2. Multi-token prediction offers similar gains without the VRAM overhead (when supported)
3. Automated tuning finds optimal settings you’d never discover manually
4. Always benchmark with warmed-up systems to get real numbers

My setup today runs circles around what I had six months ago. And the best part? When I finally do upgrade my hardware, these same techniques will scale right along with it.

Ready to double your own speeds? Download a compatible draft model for your favorite LLM, fire up llama.cpp with the flags I’ve shared, and watch your token counter soar. Your wallet — and your patience — will thank you.

*Have you tried speculative decoding? Found another optimization that works wonders? Let me know in the comments below.*