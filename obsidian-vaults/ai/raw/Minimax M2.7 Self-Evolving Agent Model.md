---
title: "Minimax M2.7: Self-Evolving Agent Model"
source: "https://www.youtube.com/watch?v=njgf43CsMDo"
author:
  - "[[Developers Digest]]"
published: 2026-03-25
created: 2026-04-21
description: "MiniMax Token Plan 12% OFF:https://platform.minimax.io/subscribe/coding-plan?code=5MBsFNv1Jf&source=linkMiniMax Platform:https://platform.minimax.ioAPI Documentation:https://platform.minimax.io/docs"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=njgf43CsMDo)

MiniMax Token Plan 12% OFF:https://platform.minimax.io/subscribe/coding-plan?code=5MBsFNv1Jf&source=link  
MiniMax Platform:https://platform.minimax.io  
API Documentation:https://platform.minimax.io/docs/guides/text-generation  
  
Minimax released M 2.7, an open source model described as the first to have deeply participated in its own evolution, with strong agentic capabilities for building complex harnesses, using agent teams, skills, and dynamic tool search. The script reviews its Artificial Analysis Intelligence Index score of 50 across multiple benchmarks and cited as 10–20x cheaper than some alternatives. It highlights Minimax’s candid benchmark reporting, including areas where it trails frontier models, while noting strong results such as outperforming Gemini 3.1 Pro on SweetBench Pro. The video explains Minimax’s self-evolution workflow and an autonomous iterative loop that improved internal programming evaluations by 30%, then demonstrates using the token plan and API (Anthropic SDK compatibility) with Opencode to generate a Next.js Developers Digest site, blog posts, and a full SaaS landing page while using minimal request quota.  
  
00:00 Minimax M 2.7 Launch  
00:27 Benchmarks And Value  
01:39 Self Evolving Agent Workflow  
03:00 Autonomous Optimization Loop  
04:01 Demos And Use Cases  
05:00 Token Plan Pricing  
05:37 API Setup And Tooling  
06:13 OpenCode Quick Start  
07:26 Nextjs Site Build Demo  
08:51 Saas Landing Page Upgrade  
10:41 Wrap Up And Takeaways

## Transcript

### Minimax M 2.7 Launch

**0:00** · MiniMax has just released M2.7, one of their latest open-source models. This is the first model that's openly talking about early echoes of self-evolution.

**0:09** · Now, what they mentioned within the blog post is M2.7 is the first model that has deeply participated in its own evolution. M2.7 is capable of building complex agent harnesses, completing highly elaborate productive tasks, leveraging capabilities such as agent teams, complex skills, and dynamic tool search. Now, when we take a look at the model on the artificial analysis intelligence index, this model scores a 50. This is an aggregate score across a ton of different benchmarks such as Humanity's Last Exam, GPQA. When we take a look at a model like this, and we compare it to some of the other state-of-the-art models, one very important aspect with the intelligence of this model is one of the big stories around models like this and M2.7 is just the price when compared to some of the latest models that are out there. This is a blended rate of 50 cents per million tokens of input and output. And when we compare this pricing to some of the other models that are out there, is this can be in the order of 10 or 20 times cheaper. So, you're going to be able to get much more performance out of this model than you would with other options that are out there. Now, when we take a closer look at the benchmark.

### Benchmarks And Value

**1:13** · Now, the one thing that I do like with the benchmarks that MiniMax provides is they don't actually show all of the benchmarks where the model just outperforms. They do they are honest with the representation in showing some areas where it isn't quite at the performance of some of the frontier models like we see on the bottom row here. But, when we compare it to some popular benchmarks like SweetBench Pro for instance, we can see that this model outperforms even the latest from Google and their Gemini 3.1 Pro model. Now, one of the really interesting things with this model is this is the first lab that I've seen openly talk building an agent from model self-evolution. This is the first time that they share an internal workflow that enables these M2 series models to self-evolve. And this is something that arguably we're going to see much more of in 2026. Now, what they describe is this workflow allows them to serve as an exploration of the boundaries of the model's agentic capabilities. And that's one thing that all of these models are really focused on right now is the agentic capabilities of what the model can actually perform.

### Self Evolving Agent Workflow

**2:13** · It's one thing to actually plot well on different benchmarks. It's another thing to actually perform things like productive real-world tasks. And what's interesting with this is you could potentially use this same type of system at a higher level with how you actually use the model. One of the interesting things that they described is during the iteration process, they realized that the model's ability to recursively evolve its own harness is also critical.

**2:35** · Our internal harness autonomously collects feedback, builds evaluation sets for internal tasks, and based on this, it continuously iterates on its own architecture. They do call out in particular skills and MCP implementations, memory mechanism to complete the task better and more efficiently. And that's one thing that's nice to see is they're actually leveraging some of these new architectures that we're seeing such as skills as well as MCP that we've seen over the past year. Now, additionally within here, what they also describe is some examples in terms of how it optimized its performance, which I do find quite interesting. They mentioned that for example, they had M2.7 optimize a model's programming performance on an internal scaffold. M2.7 ran entirely autonomously, executing an iterative loop to analyze failure trajectories, plan changes, modify scaffold code, run evaluations, and compare results, decide to keep or revert the changes for over 100 rounds. And what they found is that M2 discovered effective optimizations throughout the process, systematically searching optimal combinations. One of the most interesting aspects of this announcement that they released is what they describe is going through the process is a basically what it would do is it would run through this iterative loop. It would analyze different failure trajectories. It would plan the changes, modify the scaffold code, and run evaluations. It would compare the results and decide to keep or revert the changes. And ultimately through this iterative process, they found that this achieved a 30% improvement on internal evaluation sets. So, in this video, what I wanted to do is show you a number of different examples in terms of what the model's actually capable of doing. Now, in terms of some of the front-end capabilities, here's an example of one of the generations from the model where if you ask it to generate a website, here is an example of that. Now, in terms of where you can leverage the model, so the model is particularly strong as you might imagine within software engineering. So, if you do want to leverage this for instance for real-world programming, I'll show you a couple different demonstrations in terms of how you can leverage this. Now, the one thing that I do want to highlight with how they structured their plans, it is quite a bit different than how we typically see. So, you actually are able to get 1,500 model requests per 5 hours for $10 a month. Now, I'll leave a link to the blog post within the description of the video. Now, I actually want to show you some demonstrations of the model itself. Within the blog post, they have a handful of examples in terms of how you can leverage the model, but I wanted to go through and show you some demonstrations. So, you can leverage this from anything from building spreadsheets to actually building applications. Now, the next thing that I want to touch on, which is actually quite interesting, is how they've actually decided to price the models on what they call their token plan. For as little as $10 a month, you're going to be able to get 1,500 requests per 5 hours. And if you want to go to the $20 per month tier, you can get 4,500 model requests every 5 hours. This isn't across the month. This is every 5 hours.

### Autonomous Optimization Loop

### Demos And Use Cases

### Token Plan Pricing

**5:21** · And now, additionally, if you want the model at a higher throughput at 100 tokens per second, you will be able to pay a higher premium for that. But, in terms of the value that you get for $10, this is actually pretty amazing. There's a whole host of options with how you can get started with the token plan. Once you've signed up for the plan that you want, you can head on over and get your API key for the token plan. And then once you've done that, you have a few different options. They do have compatibility with the Anthropic SDK where for instance, if what you want to do is actually set this up within an application that you're building is you can plug in the model string for MiniMax M2.7, swap out the API key for your token plan, and then you're going to be able to just set that base URL to MiniMax, and then you can route all of the different requests to it. And now, additionally, if you want to leverage the model within a whole host of coding tools, whether it's OpenClaw, OpenCode, CloudCode, or a whole host of other harnesses, they have guides to do all of those. Now, within here, what I'm going to do is I'm going to show you how you can get started with OpenCode in particular. If I run OpenCode off login, what I can do within here is I can search for the different providers, and within here, I can search for MiniMax.

### API Setup And Tooling

### OpenCode Quick Start

**6:24** · What I can do is I can select the minimax.io. Once I've selected the model, I can go ahead and I can put in my API key. And then once I've done that, I can go ahead and I can copy my API key to put it in. And then once you've done that, you can go ahead and run OpenCode. And then once you're within OpenCode and you select models, I can search for MiniMax again, and I have all of the different models within here.

**6:43** · For instance, I can select a MiniMax M2.7, and within here, I can say hello world just to make sure that it's working. And then there we go. So, I have that response there with the thinking trace as well. Additionally within here is if you are interested in seeing how many tokens you have left with your current plan, you can see I have 1,500 requests per 5 hours for this model at the 50 tokens per second normally as well as 100 token per second off-peak. Now, what I'm going to do is I'm just going to go to my desktop. I'm going to create a new directory. I'm going to call this MiniMax M2.7 demo.

**7:13** · I'm going to go within this directory.

**7:14** · I'm going to fire up OpenCode again. And the nice thing with OpenCode is once you have set the model, it will set that as the default model every time that you go in. Once you've set this, you don't need to go in and configure the model each time. What I'm going to do within here is I'm going to say, "Create me a Next.js application. I want it to be a site on Developer's Digest. I want it to have a blog, and I want it to be within a neo-brutalist style." Let's also see the blog with a few different blog posts on TypeScript. And the one thing to know with this model is it is very good at agentic tasks. Within here, you can see it's listing out the directories. It's coming up with a plan for what it's going to build for us. It's going to run the commands to create our Next.js project. And the one thing with this model is you'll see it will begin to go through all of these tasks agentically.

### Nextjs Site Build Demo

**7:57** · Within here, I can see it's going through. It's writing some style sheets for us. It's creating all of the different post-CSS for all of the Tailwind configuration. It's going to go through. It's going to build out all of the various components. So, here we go.

**8:08** · So, here is what it has generated for us. So, within here, I can click through. I can see the different blog posts. I can see all of the different coding blocks within here. It's a starting point for what I want to continue to develop. Just to give you an idea in terms of the number of requests that it took within that agentic process that it used within OpenCode to actually generate the Next.js application. The one thing with Next.js is this isn't just something that's within a single HTML file. I'm not just asking for one request to have all of this generated.

**8:34** · It's going through and it's trying things. And the one thing to know with this with the 1,500 model requests per 5 hours is you can see with this one request, I'm just at 1%, and this is going to reset in an hour. But, actually run up on the limits even on their cheapest tier, it does seem like you are going to be able to push this model quite a bit. So, what I'm going to do within here is I'm going to say, "Convert the home page to be a SaaS landing page. I want it to be a very rich page. Let's have it with all of the different aspects that you typically see. Everything from a beautiful hero page in neo-brutalist style, all the way through to a pricing section, through to FAQs, social validation, so on and so forth. Also, add in some animations throughout the entire design." So, here is what it has generated for us. So, we have this beautiful hero section that it has created for us. Stay ahead of the TypeScript game. We have the code sample. We have start trial, so on and so forth. I have the social validation of all of the different companies, the hypothetical companies that you can include in a section like this. I have everything you need to know to master TypeScript. Just like I had in the early context of what I had asked of the model, content in and around TypeScript.

### Saas Landing Page Upgrade

**9:37** · In terms of the overall design sensibilities and the neo-brutalist style that I had asked for, I asked this type of question of a lot of different models, and this is definitely a very impressive generation. If I take a look here, I can see we have these functional FAQ sections as well. And now, if I take a look and I refresh the token usage, I am still only at 2%. So, if I take a look through this, it was able to go through and write all of this code, all of these different components for what it has on this main page here. And so, that's just to give you a glimpse in terms of some of its capabilities, but the model is able to do much, much more.

**10:10** · You're going to be able to create things like spreadsheets, PowerPoints. You're going to be able to create documents, a bunch of real-world work you're going to be able to actually do with this model.

**10:18** · Because of its agentic capability, actually being trained on these agentic capabilities, you're going to be able to use it within a whole host of ecosystems. And another interesting use case for this token plan is you could potentially also leverage it within your OpenClaw Orchestrators. You can set this to be the main model that you have to delegate all of the different tasks. For anyone that does use OpenClaw, you can potentially leverage this as an option as well. So, all in all, there's a ton of different applications in terms of how you can leverage the model. Kudos to the team and MiniMax for what they've created. From the self-evolving, early echoes of self-evolution like they described within the blog post, but through to actually the quality as well is the speed and price of the model, it's all a very compelling option. So, otherwise, that's it for this video. If you found this video useful, please like, comment, share, and subscribe.

### Wrap Up And Takeaways

**11:03** · Until the next one.