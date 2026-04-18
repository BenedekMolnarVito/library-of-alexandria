---
title: "I Cut Claude Code’s Output Tokens by 75%. Why Did Nobody Tell Me?"
source: "https://medium.com/vibe-coding/i-cut-claude-codes-output-tokens-by-75-why-did-nobody-tell-me-3275138852e2"
author:
  - "[[Alex Dunlop]]"
published: 2026-04-11
created: 2026-04-18
description: "A free Claude Code plugin cuts output tokens by 75%. A 2026 paper shows brief AI responses improve accuracy by 26 points. Install in one command."
tags:
  - "clippings"
---
## [Vibe Coding](https://medium.com/vibe-coding?source=post_page---publication_nav-413d50faa755-3275138852e2---------------------------------------)

[![Vibe Coding](https://miro.medium.com/v2/resize:fill:48:48/1*nD0mORiSRPKPztpAByfNdw.png)](https://medium.com/vibe-coding?source=post_page---post_publication_sidebar-413d50faa755-3275138852e2---------------------------------------)

Vibe Coders is where we share ideas that help shape the future.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*JMSxwQX3sJpPkXz998-5bA.png)

Image made with MidJourney, edited in Figma

## Fewer tokens. Somehow more accurate. There’s a paper.

Claude Code is **charging** you for words like “ *Certainly* ”.

**Not a fix. Not code.** *“Certainly”*, *“Sure, I’d be happy to help with that”, and “The issue you’re experiencing is most likely caused by…”. We are paying for this.*

*Allen Iverson once got roasted for going on a rant about practice. Not the game. Practice.*

Allen Iverson talking about practice.

*Here we are paying for practice words.*

*Not a Medium member? Read for free by* [***clicking here***](https://medium.com/@alexjamesdunlop/i-cut-claude-codes-output-tokens-by-75-why-did-nobody-tell-me-3275138852e2?sk=d771d9e2b416f6b60c87c12f76384a93)*.*

## The Test I Ran

I took the same Unity UI element bug. Asking Claude Code to explain it twice.

- *Default Claude Code:* **1,252 tokens.**
- *With the fix:* **410 tokens***.*

*The same fix. The same answer.*

The main difference one of them spent an **extra 800** tokens, *saying fluff*.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*arzZ8dO95ZznfzQ8E5U3HQ.png)

Examples of caveman outputs.

## The Fix Is Insanely Simple

There is a *free* [*GitHub plugin*](https://github.com/JuliusBrussee/caveman?tab=readme-ov-file) with **13,000+ stars**, that makes Claude talk like a **caveman**.

*One simple plugin, that instantly starts saving you money.*

This isn’t a joke, *April fools was 10 days ago*.

Caveman saying Me Like

```c
claude plugin marketplace add JuliusBrussee/caveman
claude plugin install caveman@caveman
```

*That’s it, one simple install, then run* `*/caveman*`*, now the caveman is active.*

![](https://miro.medium.com/v2/resize:fit:1224/format:webp/1*GE3GtnEc2NAasatyYrS6gQ.png)

caveman do

## What Caveman Claude Actually Looks Like

***Before*** *caveman is active.*

> “Sure! I’d be happy to help you with that. The issue you’re experiencing is most likely caused by your authentication middleware not properly validating the token expiry. Let me take a look and suggest a fix.”

***After*** *caveman is active.*

> “Bug in auth middleware. Token expiry check use `<` not `<=`. Fix:"

Not only does that **save** you **money**, but which one is **easier** to **read**?

## The Part That Surprised Me

I really expected there to be a trade off.

You’d think *less tokens*, means *worse output* *(right?)*.

**Wrong**, a paper called *“* [*Brevity Constraints Reverse Performance Hierarchies in Language Models*](https://arxiv.org/abs/2604.00025) *”* found the opposite. Brief responses improve accuracy by **26%** on **benchmarks**.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*G_An-7h-wH78yiPl8-Mg8A.png)

*Verbose answers aren’t smarter, they are* ***more expensive****.*

## Pick Your Level Of Caveman

*There are* ***3 modes*** *to pick how caveman you want to go.*

- **Lite** `/caveman lite`: *trims a bit, keeping grammar, still professional*.
- **Full** `/caveman full`: Default, drops articles, using fragments.
- **Ultra** `/caveman ultra`: Abbreviates everything. One word *(one word enough).*

There is also Classical Chinese mode for maximum compression. *Another reason I should have stuck to Chinese at school*.

## Some Interesting Benchmarks

Here are some stats from Julius Brussee.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*kXRdslTPcfD7kVltrDk10A.png)

Julius benchmarks

*The savings come from Claude explaining something.*

## Another Cool Simple Plugin

There is another companion tool called `caveman-compress`.

Because `CLAUDE.md` **loads** every **session**, this file is **extremely expensive**. *Every token costs you for every session.*

*Caveman Compress rewrites into a better format. Giving a human readable backup.*

Some reported savings are around: 45%.

Input tokens are important to save on too.

## What I Changed

I installed and now activate `/caveman` on every session. I love the concise outputs.

I also used to compress my `CLAUDE.md` using Claude, however now I use the new plugin. My limit hitting has gone down a lot.

I think this should be the default, *but more usage means more money for them*.

## Start By Doing This

If you have **5 minutes:** *Install the plugin. One command, use it always.*

```c
claude plugin marketplace add JuliusBrussee/caveman
claude plugin install caveman@caveman
```

If you have **15 minutes**: *Run* `*/caveman ultra*` *on your next session. Check your token count.*

If you have **30 minutes**: *Run* `*caveman-compress*` *on your CLAUDE.md. This should save you 45% alone.*

The plugin is free. Julius Brussee built it.

*Check out and star the repo, he deserves it:* [*Github repo*](https://github.com/JuliusBrussee/caveman?tab=readme-ov-file)*.*

*I am not affiliated with Claude or the Caveman project. All thoughts are my own.*

[![Alex Dunlop](https://miro.medium.com/v2/resize:fill:60:60/1*uybQ98Ulg8xZgz9X6V5mBw.jpeg)](https://medium.com/@alexjamesdunlop?source=post_page---post_author_info--3275138852e2---------------------------------------)[3 following](https://medium.com/@alexjamesdunlop/following?source=post_page---post_author_info--3275138852e2---------------------------------------)

Engineer at Popp AI. Volunteer at Aruuri. Passionate about learning/collaborating. Trying to leave a positive contribution for the dev community.

## Responses (12)

Benedek Molnar

What are your thoughts?

```c
Try https://github.com/rtk-ai/rtk, the High-performance CLI proxy that reduces LLM token consumption by 60-90%
```

53

```c
I read about it. But it seems to short for me. I actually need some explanation now and then..
```

19

```c
Did you run that past Cyber? Gone are the days we trust random repos.
```

18

[View list](https://medium.com/@molnar.benedictus/list/reading-list?source=post_page---list_recirc--3275138852e2-----------predefined%3Afb06a7b34edd%3AREADING_LIST----------------------------)