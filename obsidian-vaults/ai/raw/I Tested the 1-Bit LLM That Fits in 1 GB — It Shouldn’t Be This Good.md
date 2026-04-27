---
title: "I Tested the 1-Bit LLM That Fits in 1 GB — It Shouldn’t Be This Good"
source: "https://levelup.gitconnected.com/i-tested-the-1-bit-llm-that-fits-in-1-gb-it-shouldnt-be-this-good-3112d2825abc"
author:
  - "[[Chew Loong Nian - AI ENGINEER]]"
published: 2026-04-07
created: 2026-04-23
description: "I Tested the 1-Bit LLM That Fits in 1 GB — It Shouldn’t Be This Good A Caltech startup just crammed 8.2 billion parameters into 1.15 GB. I benchmarked it against Llama 3.1, Qwen 3, and Gemma 4 …"
tags:
  - "clippings"
---
A Caltech startup just crammed 8.2 billion parameters into 1.15 GB. I benchmarked it against Llama 3.1, Qwen 3, and Gemma 4 — and the results broke my mental model of how LLMs should work.

Three days ago, a company called PrismML emerged from stealth and dropped something that made me do a double-take: an 8-billion-parameter large language model that fits in just 1.15 GB of memory.

For context, a standard FP16 model with the same parameter count needs roughly 16 GB. PrismML’s Bonsai 8B is 14x smaller. And it doesn’t just run — it runs *fast*. On an iPhone 17 Pro Max, it clocks 44 tokens per second. That’s real-time conversation speed on a phone, no cloud required.

I had to test this myself. Because if these numbers are real, everything we thought we knew about the size-performance tradeoff in LLMs needs to be reconsidered.

## What Makes Bonsai 8B Different

Most LLMs store their weights as 16-bit or 32-bit floating point numbers. Even aggressive quantization typically brings this down to 4-bit (Q4) or 2-bit representations. Bonsai 8B goes all the way down to **1 bit**.

That means every weight in the model is constrained to essentially binary values. If you’ve been following Microsoft’s BitNet research, you’ll recognize the concept — but PrismML claims they’ve cracked the commercial viability problem that kept 1-bit models in the research lab.

The key innovation is what PrismML calls their “native 1-bit training” approach. Unlike post-training quantization (where you take a full model and compress it, losing quality), Bonsai was trained from scratch with 1-bit constraints baked in. The model never knew anything but 1-bit weights — and that apparently makes all the difference.

## My Test Setup

I wanted a fair fight, so I ran Bonsai 8B against four popular models in the same parameter class:

• **Llama 3.1 8B** (Meta’s workhorse, FP16–16.07 GB)  
• **Qwen 3 8B** (Alibaba’s multilingual powerhouse — 16.38 GB)  
• **LFM2 8B** (Liquid AI — 16.07 GB)  
• **Ministral 3 8B** (Mistral’s compact model — ~16 GB)

And the challenger:  
• **Bonsai 8B** (PrismML, 1-bit — 1.15 GB)

I tested across six standard benchmarks that cover instruction following, math reasoning, coding, function calling, multi-step reasoning, and general knowledge: IFEval, GSM8K, HumanEval+, BFCL, MuSR, and MMLU-Redux.

## The Results

Here’s the benchmark comparison table that made me question reality:

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*KI6rYKctFhC1M_7a0ywCRQ.png)

Let me break down what’s surprising here.

**Bonsai 8B scored 70.5 average — while using 14x less memory than every competitor.**

It outright beats Llama 3.1 8B (67.1) and LFM2 8B (69.6). It essentially ties with Olmo 3 7B (70.9) and Ministral 3 8B (71.0). The only model that significantly beats it is Qwen 3 8B at 79.3 — but Qwen requires 14x more memory to do it.

Look at the GSM8K math score: Bonsai hits **88.0**. That’s higher than Llama 3.1’s 76.6, higher than Olmo 3’s 84.5, and just behind Qwen’s 91.1. A 1-bit model doing math this well shouldn’t be possible — but here we are.

## The Intelligence Density Metric

PrismML introduced a metric they call “intelligence density” — benchmark score per gigabyte of model size. This is where Bonsai gets truly ridiculous:

**Model | Avg Score | Size (GB) | Intelligence Density (score/GB)**

**Bonsai 8B** | 70.5 | 1.15 | **1.062**

Qwen 3 8B | 79.3 | 16.38 | 0.098

Llama 3.1 8B | 67.1 | 16.07 | 0.084

Bonsai’s intelligence density is **10.8x higher** than the next closest model. You could argue this metric favors smaller models by design — and you’d be right. But the gap is so massive that it’s hard to dismiss. This model squeezes more capability per byte than anything else available today.

## Where It Falls Short

I want to be honest about the weak spots, because they matter.

**Coding (HumanEval+: 57.9):** This is Bonsai’s weakest benchmark. Qwen 3 8B scores 79.9 on the same test — a 22-point gap. If your primary use case is code generation, Bonsai isn’t your model. The 1-bit weight constraint seems to hurt most on tasks requiring precise syntactic output.

**Multilingual performance:** Independent community benchmarks on GitHub (ArmanJR’s Bonsai-vs-Qwen3.5 comparison) found that Bonsai struggles with non-English tasks. It’s a specialist for English workloads, not a multilingual generalist.

**Reasoning depth (MuSR: 64.3):** While decent, this score lags behind Qwen’s 70.0. For complex multi-step reasoning chains, the 1-bit precision ceiling becomes visible.

## How to Run It Yourself

Getting Bonsai running locally is surprisingly straightforward. Here’s the quickest path:

**Option 1: The official demo**

```c
git clone https://github.com/PrismML-Eng/Bonsai-demo.git
cd Bonsai-demo
export BONSAI_MODEL=8B
./setup.sh
```

**Option 2: llama.cpp (PrismML’s fork)**

```c
git clone https://github.com/PrismML-Eng/llama.cpp
cd llama.cpp
cmake -B build && cmake --build build -j
./build/bin/llama-cli -m Bonsai-8B.gguf -p "Explain quantum computing in simple terms" -ngl 99
```

==**Option 3: Ollama (community)**==

```c
ollama pull digitsflow/bonsai-8b
ollama run digitsflow/bonsai-8b
```

The GGUF file is 1.16 GB on disk. It runs natively on Apple Silicon via MLX and on NVIDIA GPUs via CUDA. I tested on an M3 MacBook Pro and it loaded in under 2 seconds.

## Why This Matters for the LLM Ecosystem

The implications of viable 1-bit models extend far beyond “cool demo”:

**Edge AI becomes real.** We’ve been talking about running LLMs on phones and IoT devices for years. But when your model needs 16 GB of RAM, that’s a non-starter for most hardware. At 1.15 GB, Bonsai 8B fits comfortably on a Raspberry Pi. PrismML reports 44 tokens/second on an iPhone 17 Pro Max — that’s faster than most cloud API responses.

**Cost collapses.** If you’re serving an 8B model, the GPU memory required just dropped by 14x. That means 14x more concurrent users per GPU, or the ability to run on dramatically cheaper hardware. For startups building AI products, this changes the economics completely.

**Privacy by default.** When the model runs locally on the device, user data never leaves the phone. No API calls, no cloud logging, no privacy policy headaches. For healthcare, legal, and finance applications, this is massive.

**The BitNet connection.** Microsoft has been researching 1-bit architectures with BitNet since 2023, but their models stayed in the 2B parameter range. PrismML pushing this to 8B with competitive benchmarks suggests the technique scales — and we might see 70B 1-bit models that fit in under 10 GB within the year.

## The Bigger Picture

I’ve been testing LLMs for two years, and the trend has always been the same: bigger models, more GPU memory, higher cloud costs. Bonsai 8B is the first model that seriously challenges this trajectory.

Is it going to replace Qwen 3 8B for a developer who needs top-tier code generation? No. Will it replace GPT-4o or Claude for complex reasoning tasks? Absolutely not.

But that’s not the point. The point is that a 1-bit model with 8 billion parameters can score 70.5 across standard benchmarks while fitting in a gigabyte. Two years ago, that would have been science fiction.

PrismML also released Bonsai 4B and Bonsai 1.7B variants, which presumably shrink the memory footprint even further. I haven’t tested those yet, but they could be the sweet spot for truly embedded applications — think smart home devices, cars, and wearables running genuine LLM inference.

The race isn’t just about who can build the biggest model anymore. It’s about who can build the *densest* one. And right now, PrismML is winning that race by a factor of 10.

*If you found this useful, follow me for daily deep-dives into LLMs, AI agents, and the tools reshaping how we build software. I test so you don’t have to.*