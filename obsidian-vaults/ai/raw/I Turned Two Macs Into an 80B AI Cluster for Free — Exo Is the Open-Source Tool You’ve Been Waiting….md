---
title: "I Turned Two Macs Into an 80B AI Cluster for Free — Exo Is the Open-Source Tool You’ve Been Waiting…"
source: "https://medium.com/data-science-collective/i-turned-two-macs-into-an-80b-ai-cluster-for-free-exo-is-the-open-source-tool-youve-been-waiting-ffa14b8e8dc0"
author:
  - "[[Manjunath Janardhan]]"
published: 2026-03-14
created: 2026-04-18
description: "I Turned Two Macs Into an 80B AI Cluster for Free — Exo Is the Open-Source Tool You’ve Been Waiting For Running Qwen3-Next-80B at 70–80 tokens/second on a home cluster with zero cloud costs In …"
tags:
  - "clippings"
---
## [Data Science Collective](https://medium.com/data-science-collective?source=post_page---publication_nav-8993e01dcfd3-ffa14b8e8dc0---------------------------------------)

[![Data Science Collective](https://miro.medium.com/v2/resize:fill:48:48/1*0nV0Q-FBHj94Kggq00pG2Q.jpeg)](https://medium.com/data-science-collective?source=post_page---post_publication_sidebar-8993e01dcfd3-ffa14b8e8dc0---------------------------------------)

Advice, insights, and ideas from the Medium data science community

*Running Qwen3-Next-80B at 70–80 tokens/second on a home cluster with zero cloud costs*

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*wgXl-OMNzaZZ-auhV17jqA.png)

Image By Manjunath Janardhan. Snapshot of Mac Min’s setup and load.

In my last article, *“I Turned My 16GB Mac Mini Into an AI Powerhouse — Here’s How LM Studio Link Changed Everything”*, I explored using AI models on smaller machines by running Models on powerful machines using LM Studio Link.

## [I Turned My 16GB Mac Mini Into an AI Powerhouse — Here’s How LM Studio Link Changed Everything](https://medium.com/codetodeploy/i-turned-my-16gb-mac-mini-into-an-ai-powerhouse-heres-how-lm-studio-link-changed-everything-8f1f20b58f60?source=post_page-----ffa14b8e8dc0---------------------------------------)

### Running 70B parameter models on a machine that shouldn’t be able to. No cloud. No API keys. Just two Macs and an…

medium.com

What if I want to go in the other direction — pool the CPU, GPU and RAM from multiple machines to run a model none of them could handle alone?

What if you have a bunch of smaller devices lying around and you want to combine their resources to punch above their weight?

Meet **Exo**. It is the answer to exactly that question.

## What Is Exo?

Exo is an open-source project maintained by Exo Labs. In one line: it connects all your devices into a personal AI cluster, allowing you to run frontier models that would never fit on any single machine.

### Key capabilities at a glance:

- Automatic Device Discovery — devices running Exo find each other over the network automatically. No manual configuration.
- Topology-Aware Auto Parallel — Exo figures out the optimal way to split your model across devices based on available RAM, CPU/GPU resources, and network latency between each node.
- Tensor Parallelism — model sharding for up to 1.8x speedup on 2 devices and 3.2x on 4 devices.
- RDMA over Thunderbolt 5 — on supported hardware (M4 Pro/Max), this unlocks up to 99% reduction in inter-device latency.
- MLX Backend — uses Apple’s MLX framework for GPU-accelerated inference on Apple Silicon.
- OpenAI-compatible API — exposes [http://localhost:52415/v1](http://localhost:52415/v1) so any tool that speaks to OpenAI can talk to your cluster instead.
- 54+ models supported — from small Llama models to 671B DeepSeek variants.
- Works on Mac, Linux, and even Raspberry Pi.

## My Setup: Mac Mini M4 + MacBook Pro M4 Max

For this experiment, I paired two machines:

- Mac Mini M4–16GB unified memory, 55.1GB/64GB used at peak (86%)
- MacBook Pro M4 Max — 64GB unified memory, 9.8GB/16GB on secondary partition (61%)

Together, that gives the cluster enough headroom to load Qwen3-Next-80B-A3B-Thinking-4bit — a 44GB quantized model that neither machine could comfortably handle alone. The model ran at a consistent 70–80 tokens per second (TPS), with TTFT (time to first token) around 4–11 seconds depending on query complexity. Temperature: the Mac Mini peaked at 41–86°C under load, the MacBook Pro stayed cooler at 48–53°C.

## Getting Started: It’s Genuinely This Simple on Mac

For macOS, Exo ships as a native app (requires macOS Tahoe 26.2 or later for the DMG version):

- Download EXO-latest.dmg from the releases page.
- Copy it to Applications and launch.
- Repeat on every other machine on the same network.
- Done — the nodes discover each other automatically and show up in the Topology view.

**That’s it. It just works.**

## Linux and Windows Setup

Linux users need to run from source. First, install the prerequisites:

- uv (Python dependency manager):  
	curl -LsSf [https://astral.sh/uv/install.sh](https://astral.sh/uv/install.sh) | sh
- Node.js 18+ and npm
- Rust (nightly):  
	curl — proto ‘=https’ — tlsv1.2 -sSf [https://sh.rustup.rs](https://sh.rustup.rs/) | sh && rustup toolchain install nightly

Then clone and run:

```c
git clone https://github.com/exo-explore/exo
cd exo/dashboard && npm install && npm 
run build && cd ..
uv run exo
```

**One important caveat:** on Linux, Exo currently runs on CPU only. GPU support for Linux is actively under development — worth tracking if you have an NVIDIA or AMD GPU you want to throw at this.

## The Dashboard: Cluster Visibility Out of the Box

Once running, the built-in web dashboard at [http://localhost:52415](http://localhost:52415/) gives you a real-time topology view of your cluster. Each node shows its current CPU usage, temperature, power draw, and memory utilization. You can see which device is handling which portion of the model — this is the Topology-Aware Auto Parallel engine in action.

Before downloading, it displays the combined RAM and the model that can run in your AI Cluster.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*CgLwV3y9Frbs8yU6kHdSOQ.png)

Image By Manjunath Janardhan. Snapshot of the Models that can be run with 80GB (64GB + 16 GB ) of RAM.

After you download and run your first prompt, models are split into layers on both machines based on each machine's RAM.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*upKZbwShZQ72s7gnKot-lA.png)

Image By Manjunath Janardhan. Snapshot of Exo redy to chat.

During inference, you can watch the Mac Mini spike to 97% CPU at 86°C and 82W while the MacBook Pro hums along at 8–13% — Exo is smart enough to distribute the workload based on available resources. The THINK mode in the dashboard enables chain-of-thought reasoning, which you can expand or collapse after generation.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*nKt_EgkbqHNAWz90_855hw.png)

Image by Manjunath Janardhan. Snapshot of Exo when Running!

## The API: Drop-In OpenAI Replacement

Exo exposes a fully OpenAI-compatible REST API at [http://localhost:52415/v1.](http://localhost:52415/v1.) That means any tool, agent framework, or application that supports the OpenAI SDK can point to your local cluster instead — no code changes needed.

A quick example using curl:

```c
curl -N -X POST http://localhost:52415/v1/chat/completions \
  -H 'Content-Type: application/json' \
  -d '{
    "model": "mlx-community/Qwen3-Next-80B-A3B-Thinking-4bit",
    "messages": [
      {"role": "user", "content": "What is sky blue ?"}
    ],
    "stream": false
  }'
```

We will receive the JSON output as shown below.

```c
{"id":"887aab7d-c2e4-455d-bb7e-44d82b998bb1","object":"chat.completion","created":1773493013,"model":"mlx-community/Qwen3-Next-80B-A3B-Thinking-4bit","choices":[{"index":0,"message":{"role":"assistant","content":"\n\nThat's a great question! The phrase \"sky blue\" can mean two things, depending on context:\n\n### 1. **The Color \"Sky Blue\" (as a Name)**  \n   - This refers to a specific **pale, soft shade of cyan or light blue** — like the color of a clear daytime sky on a sunny day.  \n   - In digital design, it’s often defined as:  \n     - **Hex code: \`#87CEEB\`**  \n     - **RGB values: (135, 206, 235)**  \n   - It’s a common color name used in art, fashion, and design to describe a gentle, calming blue reminiscent of a cloudless sky.\n\n---\n\n### 2. **Why the Actual Sky Is Blue (The Science!)**  \nThis is the more fascinating part — and the reason the color is *named* \"sky blue\" in the first place! The sky appears blue due to a phenomenon called **Rayleigh scattering**:  \n\n- **Sunlight = White Light**: The sun emits all colors of light (red, orange, yellow, green, blue, violet), which combine to make \"white\" light.  \n- **Earth’s Atmosphere**: When sunlight enters our atmosphere, it collides with gas molecules (nitrogen, oxygen) and tiny particles.  \n- **Scattering by Size**: Shorter wavelengths (like **blue and violet**) scatter more easily off these molecules than longer wavelengths (red, yellow).  \n  - Blue light has a wavelength of ~450–495 nanometers — small enough to bounce around in all directions.  \n  - Violet light scatters even more, but our eyes are less sensitive to violet, and the sun emits less violet light to begin with. So **blue dominates** what we see.  \n- **Result**: When you look up at the sky (away from the sun), you see this scattered blue light coming from all directions → the sky appears blue!  \n\n#### 🌅 Why Sunsets Are Red/Orange:  \nAt sunrise/sunset, sunlight travels through *more* atmosphere to reach your eyes. Most blue light gets scattered *away* before reaching you, leaving the longer red/orange wavelengths to dominate the sky near the horizon.\n\n#### ❌ Common Misconception:  \n> *\"The sky is blue because it reflects the ocean.\"*  \nThis is **false**! The ocean appears blue *because* it reflects the sky’s blue color — not the other way around. The sky’s blue color comes from atmospheric scattering, not water.\n\n---\n\n### Key Takeaway:  \n- **As a color name**: \"Sky blue\" is a specific pale blue shade used in design.  \n- **In nature**: The sky looks blue because Earth’s atmosphere scatters short-wavelength blue light more than other colors.  \n\nThis is one of nature’s most beautiful examples of physics in action! 🌈 If you’re curious about anything else about light, color, or the sky, just ask! 😊","reasoning_content":"Okay, the user asked \"What is sky blue?\" Hmm, this seems straightforward but I need to unpack it carefully. \n\nFirst thought: They might be literally asking about the color name \"sky blue\" as a pigment or digital color code. But that feels too shallow—why would someone ask that? Probably not. \n\nSecond thought: Maybe they're curious about why the sky is blue scientifically. That makes more sense for a general question. But I should check if they're a child or adult—the phrasing is very simple, so could be either. \n\n*Pauses* Wait, the question is phrased as \"What is sky blue?\" which is ambiguous. Could mean: \n- The definition of the color term \n- The science behind sky color \n- Or even a metaphorical meaning? Unlikely. \n\nGiven how common this is, 90% chance they want the Rayleigh scattering explanation. But I should confirm by covering both angles. \n\n*Checks mental notes* \n- Color definition: sky blue is a pale cyan shade, hex code #87CEEB etc. \n- Science: nitrogen/oxygen scattering short blue wavelengths more than red. \n- Bonus: why sunsets are red (different scattering length). \n\nUser probably doesn't need the hex code unless they're a designer. But if they are, I'll include it just in case. \n\n*Potential pitfalls*: \n- Don't say \"blue because of the ocean\"—common myth. Must clarify it's the other way around. \n- Avoid jargon like \"Rayleigh scattering\" without explaining simply. \n- Mention why space is black but sky is blue? Maybe overkill. \n\n*Structure plan*: \n1. First answer the science part simply (main focus) \n2. Then note the color name meaning briefly \n3. Address the ocean misconception if it comes up naturally \n4. End with sunset contrast for extra clarity \n\n*User's possible deeper needs*: \n- Maybe saw a weird sky color and got curious? \n- Could be a kid doing homework. \n- Or adult refreshing basic science. \nNo need to overcomplicate—just give clear, friendly facts with \"why it matters\" context. \n\n*Double-checking*: \n- Yes, Rayleigh scattering is correct for daytime blue sky. \n- Ocean reflection is a myth—that's why the sky isn't blue everywhere (e.g., Mars has reddish sky). \n- Should I mention Mie scattering for clouds? Maybe not unless asked. Keep it focused. \n\nFinal decision: Lead with the science explanation as primary answer, add color definition as secondary, debunk ocean myth explicitly. Keep tone warm but precise. \"Ah, great question!\" feels right to start.\n","name":null,"tool_calls":null,"tool_call_id":null,"function_call":null},"logprobs":null,"finish_reason":"stop"}],"usage":{"prompt_tokens":15,"completion_tokens":1184,"total_tokens":1199,"prompt_tokens_details":{"cached_tokens":0,"audio_tokens":0},"completion_tokens_details":{"reasoning_tokens":0,"audio_tokens":0,"accepted_prediction_tokens":0,"rejected_prediction_tokens":0}},"service_tier":null}
```

This is what makes Exo powerful for developers. You can wire it into Agentic AI Applications, LangChain, LlamaIndex, your own agentic pipelines, or any OpenAI-compatible client. Your local cluster becomes a private inference endpoint.

## RDMA over Thunderbolt 5: The Next Level

If you have M4 Pro or M4 Max hardware with Thunderbolt 5, Exo supports RDMA (Remote Direct Memory Access) — a capability new to macOS 26.2. This reportedly delivers up to a 99% reduction in inter-node latency, enabling the kind of performance you would normally associate with data center interconnects.

I could not test this in my current setup (RDMA Not Enabled warning is visible in my screenshots — my machines are on WiFi, not Thunderbolt 5), but the benchmarks from Jeff Geerling’s 4× M3 Ultra Mac Studio cluster show Qwen3–235B running at production-grade speeds. That is the ceiling of what this tool can become.

## Real-World Performance Numbers

Here is what I observed across my test queries:

- “Why is Sky Blue?” — TTFT: 10,739ms, TPS: 75.2 tok/s (13.3 ms/tok)
- “Write a snake game in Python” — TTFT: 4,049ms, TPS: 69.1 tok/s
- General inference: sustained 68–75 TPS across sessions

For an 80B parameter thinking model running entirely on local hardware with zero cloud costs, these numbers are genuinely impressive. The THINK mode (chain-of-thought reasoning) adds to TTFT as expected, but the model quality is noticeably stronger with it enabled.

## Exo vs. LM Studio Link: When to Use Which

These two tools solve adjacent but distinct problems:

- *LM Studio Link* — use when you have one powerful machine and want to access it from weaker devices on your network. One host, many clients.
- *Exo* — use when you want to combine multiple machines into a single virtual GPU cluster. Many hosts, one model.

If your goal is to run bigger models than any individual machine supports — Exo is the right tool. If your goal is convenience and remote access — LM Studio Link remains excellent.

## Final Thoughts

Exo is one of the most practical open-source AI tools I have come across. The barrier to entry is remarkably low — especially on Mac — and the ceiling is remarkably high. Running a thinking-capable 80B model at home, distributed across two laptops on the same WiFi network, would have sounded like fiction two years ago.

If you are building agentic AI systems, running local experiments, or simply curious about what your hardware can do when it works together, give Exo a try. The setup will take you two minutes in Mac. The implications will keep you busy much longer.

## Reference

## [GitHub - exo-explore/exo: Run frontier AI locally.](https://github.com/exo-explore/exo?source=post_page-----ffa14b8e8dc0---------------------------------------)

### Run frontier AI locally. Contribute to exo-explore/exo development by creating an account on GitHub.

github.com[Exo](https://medium.com/tag/exo?source=post_page-----ffa14b8e8dc0---------------------------------------)[Ai Cluster](https://medium.com/tag/ai-cluster?source=post_page-----ffa14b8e8dc0---------------------------------------)