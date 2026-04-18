---
title: "Openclaw + Gemma 4 = FREE & Private AI"
source: "https://www.youtube.com/watch?v=YVh7HOw7EGk"
author:
  - "[[Jimi Barkway | AI Automation]]"
published: 2026-04-13
created: 2026-04-18
description: "📈 ALL Systems: https://go.jimibarkway.com/skoolDiscover how to build your own private AI assistant using Google's Gemma 4, Olama, OpenClaw, and SEA XNG. Dit..."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=YVh7HOw7EGk)

## Transcript

**0:00** · Imagine if you had your own AI assistant that searches the web, works completely autonomously to grow your business and costs absolutely nothing. Running entirely on your computer completely privately with zero data leaving your device. In this video, I'm going to show you exactly how to set up Gemma's brand new Gemma 4 model with Ollama, Open Claw and a private search engine called SearXNG.

### Introduction to Gemma 4 and Private AI

**0:23** · So you can ditch your ChatGPT subscription for good, keep your business data completely private on your own hardware and have a fully working AI assistant set up in minutes, even if you've never touched a terminal in your life. And if you don't know who I am, my name is Jimmy Barqueway. I run an AI startup. So if you haven't already, grab yourself a fresh cup of tea and let's dive straight in.

**0:44** · So to follow along with this, quite simple, just come to my community link down below.

**0:48** · And then come into the classroom down to the AI Vaults.

**0:54** · And it's this link right here. So you can just go ahead and click this Notion guide.

**1:00** · And you've got a complete A to B Notion guide walking you through everything including all the terminal commands, how to set up Open Claw, everything we need. So what are we building here? Open Claw and Gemma 4 and SearXNG, build your free and private AI assistant. So all of your data is going to stay on your computer forever. No more subscriptions with this.

### Building a Free and Private AI Assistant

**1:22** · And Gemma 4 is built for agentic workflows. So it's perfectly built for agents like Open Claw to be running your business on autopilot. Cloud models like Claude's, ChatGPT, Perplexity, even Gemini's models start to rack up quickly when they're using them as a backbone for your business. And not only that, the privacy issue is growing more and more.

**1:45** · So every bit of data that goes through an AI chatbot is going through these private companies' servers and ultimately that is not good enough for security for your business. You can't really opt out. So the solution is a free open-source model that runs entirely on your machine with private web search built in, no accounts, no tracking, zero dollars per year. So we're using Google's latest open model Gemma 4 released just a few days ago and it runs on 8 GB of video RAM.

**2:15** · But if you have Windows, then you will need to have at least 8 GB of video RAM on your video card. We're going to be using Ollama to set this up because it does all of the heavy lifting when it comes to actually pulling in these open-source models and getting them set up on Open Claw nice and easy.

### Using Olama to Set Up Gemma 4

**2:33** · And we'll use Open Claw to chat with our AI. You can do this through WhatsApp, Telegram, Discord.

**2:40** · They're absolutely massive with 310,000 GitHub stars. You've probably heard of them.

**2:45** · Then we'll be using SearXNG for our web search. It is a private metasearch engine, aggregates 24/7 sources across Google, DuckDuckGo, across lots of different search engines and aggregates all of that bringing it back to your Open Claw. So there's four different models in the Gemma series. The top two were built for mobile devices or laptops with less video RAM and the bottom two there were built for slightly higher end machines, but all of it is built to be able to run at home.

**3:17** · So you don't need commercial level hardware, giant servers to be able to run these open-source models anymore.

**3:23** · Gemma 4 has made it accessible enough so that we can run these on our own machines. So depending on how much video RAM you have will depend on which model you're going to go for. Now, a quick tip on this, Gemma 4 26B, the reasoning on this is basically as good as Gemma 4 31B. Although this is the more powerful model, 31B, it is significantly slower.

**3:52** · So 26B has been designed for speed. If you want your Open Claw to be answering quickly, then that's the model I would recommend going with and that's what I'm going to go with today. I'm going to get this set up. But if you don't mind waiting and you want the slight boost in reasoning then you can go for 31B instead. Let's get started.

**4:10** · So before we jump in, let me just walk you through these different models so you can see they've got E2B and E4B made for mobile and then 26B and 31B as the other two models that are more built for desktop or laptop machines with enough video RAM. They are built for agentic workflows, multimodal reasoning, they can read audio, video, lots of different formats, which is massive for agents like Open Claw.

**4:36** · And stick around to the end of the video if you want to see some use cases that I'm actually using in my business for Open Claw. And you can see here how the model performs versus its actual size. So it's basically on par with some of the best open-source models, but the size of it is significantly smaller so that it can actually be run on the hardware you have at home. And coming down a bit further, you can see here's all the ways we can download it.

**5:05** · We're going to be using Ollama today cuz they make it so straightforward. So you can think of Ollama as the engine for your AI. It makes it ridiculously easy to install these models. So you just want to start by downloading this. For that, you can just come to ollama.com like so, copy this terminal command and don't be intimidated by the terminal at all cuz all you're doing is copy and pasting. Downloading Ollama for us automatically detects what your OS is.

**5:34** · It'll ask for your password. Going to resize this a bit so you can see it better. Now, once that's done, you can just type in Ollama. So we're going to use Google's new Gemma 4 E4B model and it's super efficient. The crazy thing about these new models is the massive 256K context window. If you don't know what that means, then the context window is just the AI's short-term memory. A 256K window means that you can paste entire books or hundreds of PDF documents into the chat and the AI will actually remember all of it whilst you're talking to it. So just copy these next commands.

**6:04** · We're going to pull in the Gemma 4 model.

**6:09** · Just like that and it's going to download. It'll be about 9.6 gig. And then this model is going to live on your video RAM and that and that is why it is able to answer you so quickly and run autonomously with some speed. Once that's done, you can just run Ollama list to verify. Yes, we've got Gemma 4, the E4B model, 9.6 gigabytes in size.

### Wiring Up Gemma 4 with OpenClaw

**6:31** · Now, let's wire it up so that we can actually chat with it with an Open Claw.

**6:35** · Now, once that's done, you want to come over to Open Claw and for the rest of this we we can actually ask Claude to get this set up for us. So let's go ahead and copy the URL up here.

**6:45** · Come over to a new Claude session. You can select a new folder. Just give it a blank directory right here and then select the Opus 4.6 model for the best coding ability and just paste in openclaw.ai right there. Hey Claude, I've got Gemma 4 E4B loaded into my Ollama so that I can use this as an open-source model. I want you to install Open Claw on my computer so that I can use the Gemma 4 open-source model as the reasoning AI model for Open Claw.

**7:16** · Run all terminal commands that are necessary, go through the configuration and I want to see the Open Claw configuration open up in a terminal window so that I can go through it myself. Install all dependencies, everything needed to get this up and running. Let's go. So I've set this to bypass permissions because I just want it to go autonomously without stopping to ask me for permissions every time.

**7:41** · Now, if you don't trust Claude's then you can just set this to ask permissions and it'll go ahead and tell you exactly what it's changing, what commands it's running, that sort of thing. Now, while that's running, if you don't have Claude codes, the desktop app, then you can just come over to claude.com/download and download that for your OS. So it's installed Open Claw for me and now it's opening the terminal so we can go through the onboarding. Okay, Open Claw is installed and the onboarding is running in the terminal. Here's what I've set up, Open Claw, a path to Open Claw and the Ollama API key as well.

**8:16** · Ollama server running and the model is set up as well.

**8:20** · The onboarding wizard is now running in the left terminal window. It's asking you about the security/trust model.

**8:25** · Here's what to do as you go through it.

**8:26** · Current screen, it's asking if you understand it's personal by default.

**8:30** · Select yes to continue. Okay, let's go through the onboarding. I understand this is personal by default and shared multi-user use requires lockdown.

**8:38** · Okay, just look at it a bit higher.

**8:40** · Yeah, we're going through the Open Claw setup. Yes, continue. Go for quick start. Now, the model, this is the important bit so listen close. You want to come down until you get to Ollama.

**8:51** · Claude Code has already set up Ollama with the Gemma 4 model.

**8:56** · So as soon as you select this, it will be using Gemma 4 and the Ollama base URL is ending in 11434.

**9:05** · Just double-checking in Claude Code, it is the same. So all good. And there's a couple of options. You can either run it in the cloud and local or you can just run it locally.

**9:16** · Now, Ollama do have a cloud subscription. But if you want to keep this completely free, then you can just go with the local model and that's what I'm doing today. And it's asking me to set up the default model. We're just going to keep the current one which is Gemma 4. For the channel, you can set this up with any way that you want to be talking to Open Claw. I'll probably go with Telegram, but for now, I'm just going to skip this for now just so that we can go ahead and start using Open Claw and get to these use cases. And for a search provider, you're going to come down to SearXNG for a fully private, self-hosted search.

### Private Web Search with SIA XNG and Docker

**9:50** · Right now, your AI is smart, but it doesn't know what's happening today.

**9:53** · If you want private web search using SearXNG to do this, We need a developer tool called Docker.

**10:00** · If you're new to Docker, don't sweat it.

**10:01** · Docker is basically a virtual shipping container for software. It allows you to download a complex program like CXNG, and you can run it instantly.

**10:10** · You don't even have to mess around with any installations. And to do that, we're going to come back to Claude Code and simply ask it to do it for us. Hey Claude, I need a CXNG base URL to paste into my Open Claude config terminal. And to do this, I want you to set up CXNG private web search in a Docker environment, install all the dependencies needed to make this happen, and do all the installations needed.

**10:36** · Once done, give me the base URL, and I will paste it into the Open Claude configuration terminal myself.

**10:43** · And then send it off. So, Docker isn't installed, it's a text that automatically for us.

**10:48** · And it'll go ahead and put it together.

**10:50** · This is the beauty of having tools like Claude Code in this day and age.

**10:54** · You no longer need to wrestle with a terminal, going back and forth, trying to figure out what's wrong. You can just ask Claude, it's got full access to your computer, and it can do it for you. It's opening Docker for us.

**11:06** · And once it does, it asks you to log in to Docker, which you can do with a Google account. And now it's going to automatically pull CXNG and get that set up. And that's all done. It took about 2 minutes.

**11:18** · So, just copy the local host right here, and then we're going to come back to our terminal and paste that in.

**11:25** · And it's going to ask us if it wants us to install some skills.

**11:29** · If you don't know what a skill is, it's basically just a markdown file. It's just text.

**11:34** · But it is a specific set of instructions that turns the AI from someone who is fully relying on the knowledge of their model, which is usually only up to a certain cutoff date.

**11:49** · Instead of this, it gives them any kind of knowledge that you want to give to it. So, you can make it an expert on fishing best practices. You can make it an expert on how to build schematics for uh a new hotel you're building. It's the sky's the limit here.

**12:07** · But usually what people use it for is when you're doing a repetitive task, and you don't want to constantly have to do the same thing over and over again. You can just turn that into a repeatable skill, so that Claude knows exactly what to do next time we do this.

**12:21** · So, I'm just going to skip this for now, just so we can get on to the Open Claude use cases. But this is basically letting you install some tools that will allow Open Claude to do things like you can see on screen, set up reminders, have a password vault.

**12:34** · Come down a bit further, you've got things like Gemini CLI for using the Gemini AI. You can monitor your model usage, although this isn't going to matter so much because we're using open-source models. So, that's another benefit of this, it's not costing you anything.

**12:50** · And it doesn't matter how much usage you're going through, cuz it's completely free. So, we're going to skip this for now. And to do that, just press space to select skip, and then enter.

**13:00** · And then you can skip through a lot of these. I don't want to set a Google Places API just yet, or a Notion API, or an Open AI API, or an Eleven Labs API. Skip through enable hooks.

**13:13** · Press space, and and now we can in Open Claude's words, hatch our bots using the Now, you can do it in the terminal user interface or the web UI.

**13:22** · I'm going to do web user interface, just cuz it looks a lot cleaner. And here we have our Open Claude chatbot set up. I'm going to put this into light mode, and you can see we've got our Gemma 4 Lama model set up right there.

**13:35** · And let's start off by saying, "Hey Open Claude, how's it going today?" Send that off. Now, the first message is going to take about 10 to 20 seconds, but this is just while Gemma 4's getting set up. All the other messages after this are going to be much quicker. "I'm online, processing smoothly, and ready for whatever you have lined up. What's the focus for today?" So, let's test this out, and to really show what this free setup can do. So, first, let's turn a 2-hour research task into a 10-second automated workflow.

### Automated Workflow Example with OpenClaw

**14:01** · I'm going to have our AI use CXNG to research the very model that we're using right now, Gemma 4, and turn it into a newsletter for me.

**14:10** · "Search the web for the latest updates on Google's new Gemma 4 open-source AI model. Read the top three results, and write a highly engaging three-paragraph email newsletter summarizing the news.

**14:23** · Format it with emojis and bullet points to make it fun to read. And write as if you're talking to a smart best friend."

**14:29** · And we'll send it off. Okay, so it's pulled up some search results for us.

**14:32** · Gemma 4 is positioned as their most capable open models yet.

**14:36** · It's built with the same tech as Gemini 3, and it aims to be the industry's best open proprietary combo. It's being fully integrated into the Google Cloud ecosystem, specifically available on TPUs via Vertex AI.

**14:49** · Or in our case, Open Claude. And it's written us a nice newsletter there, which we can ask it to elaborate on, make it longer, shorter, different tone, whatever you want to do here. Now you have it, a completely free and private AI that can run Open Claude for you on your own machine using Google's latest open-source models. Now, Open Claude isn't the only autonomous model that you can use.

**15:13** · Now, if you have a Claude subscription, and you want to know how to run your computer completely autonomously without you even needing to be there, then check out this video right here.