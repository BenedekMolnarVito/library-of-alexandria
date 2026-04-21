---
title: "Claude Code + Karpathy's NEW Self-Evolving System = 10x Code Generation"
source: "https://www.youtube.com/watch?v=9iWTRMjbBvo"
author:
  - "[[WorldofAI]]"
published: 2026-04-06
created: 2026-04-21
description: "In this video, I show how Andrej Karpathy’s LLM Wiki — a self-evolving knowledge system — can be hooked up to Claude Code to massively supercharge your AI co..."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=9iWTRMjbBvo)

## Transcript

### Introductions

**0:00** · And Cararpathy had recently posted a tweet a few days ago about him building a self-evolving knowledge system powered by an AI model. The core idea is that instead of you writing notes or organizing your knowledge, the large language model does it for you where it can read raw data, write summaries, build structure, maintain consistency, answer questions, and improve itself over time. The tweak kind of popped off because it fundamentally makes AI agents way smarter with a self-improving system. And if you hook this up to a coding agent, it unlocks it to new doors. It's something that I'm going to be showcasing how you can set up in under 5 minutes because it's super easy and it's something that will revolutionize your AI coding agent. For example, someone actually built this in real life, a system called Farza Pedia.

### Demo

**0:51** · And this is something that took around 2,500 personal entries from things like diary notes, Apple notes, and messages.

**0:59** · And a large language model had turned it into a full personal Wikipedia with hundreds of structured articles covering friends, ideas, interests, and even creative inspirations. But the key difference is this wasn't built for the person. It was built for the agent.

**1:15** · because everything is organized as structured interlin files the agent can easily navigate and it can even pull context and use it to complete real tasks. So instead of just answering questions, it can do things like help design a landing page by pulling from past inspirations, ideas, and experiences all automatically. And as new information gets added, the system updates itself, linking it across multiple areas or even creating entirely new pages. Basically acts like a super intelligent librarian for your brain.

### LLM Wiki Explanation

**1:50** · And that never stops organizing, connecting, and improving your knowledge. But just today, he refined the idea even further. Instead of sharing code or an app, he shared an idea file, a high-level blueprint that an AI agent can take, build out, and customize for your workflow. He even posted a gist of this file so you can hand it over to an agent to create your own self-evolving knowledge system. He kept it intentionally abstract since there are countless ways to use it. This marks a big shift cuz we're moving from sharing software to sharing ideas.

**2:26** · letting AI handle the execution.

**2:28** · Combined with self-improving knowledge bases, agents can now build tools for you and continuously get smarter over time. So here's what the large language model wiki that new file that he had introduced does. This is a three layer system. You first have your raw sources.

**2:46** · This is essentially your mutable articles, notes, and data that claude code or whatever AI coding agent will use. Then you have the wiki which is the large language model generated markdown files that is constantly being updated with links and it keeps it consistent.

**3:03** · And then lastly you have the schema rules that tell the large language model how to organize update and maintain everything. You can connect it to an AI agent like cloud code point it at the index MD of your wiki and then suddenly the agent can drill into the exact pages it needs whenever you ask a question.

**3:23** · From there, the loop is simple. You add new sources, ask questions, or generate outputs, and the large English model will automatically update and improve the wiki over time. The magic is this.

**3:35** · Humans are great at exploring ideas, but bad at maintenance. Large English models handle the tedious bookkeeping, linking, and consistency. So, the knowledge base stays and keeps getting smarter and more useful automatically. So if you are to connect this large language model wiki, this new architecture to claude code, it lets your agents any AI coding agent that you connect it with to directly read, navigate and reason over structured wikis. So it can answer complex questions and generate outputs using your knowledge automatically.

**4:08** · Essentially turns Claude Code from a simple coding assistant into a self-updating contextware knowledge worker, which is essentially going to be solving a lot of the memory issues that Claude Code has. and it greatly improves the output quality as well. If you want the best AI tools, workflows, and drops before everyone else, join my free newsletter with the link in the description below, which is completely free. To get started, as Andridge had stated that for the ID, he uses Obsidian as the front end that can help you visualize the raw data as well as help you compile the data to the wiki. So, I would recommend that you install Obsidian if you don't have it already.

### Setup

**4:45** · Then make sure you have your coding agent installed and that way we can easily have it connected to it so that we can structure out this new approach.

**4:54** · After Obsidian has been installed, you'll need to create a new vault. This is essentially a local directory on your computer that is going to be holding all of your raw files and large language model generated wiki. You can choose whatever location you want. I am going to be creating and naming it this. Then what you'll need to do is open up your cloud code instance within that vault that you had just created. And I am personally going to be using cloud code within VS code as it is a lot easier for me to work and visualize all these elements. So now that you are within that cloud code instance, you'll now need to head over to the LLM wiki MD.

**5:31** · This is where you're going to need to copy each and every component of this system prompt. This is the instruction that our car pathy had generated. It's the idea file that you can paste into your large language model like a prompt and essentially once you have copied it, you can then paste it into your cloud code instance. After copying carpathy's gist file, the idea file, you can paste it into obviously the cloud code agent or whatever AI agent that you're using, but you're going to need to provide a better prompt to help it implement it.

**6:02** · Now I know most people will just simply type in implement the large English model knowledge base LM wiki implementation plan within Obsidian. But if you are to provide a better detailed instruction, it is going to allow the agent to build everything with a proper structure with the initial script prompt and workflow based off of the rule set that Andre had set up. So I'll leave this instruction in the description below. And then what you can do is just send it in to your cloud code agent. And this is where it is going to now set up the idea file with instructions that were given to generate the complete large distish model wiki. And it is going to be then set up within Obsidian.

**6:42** · This is where it is going to create the first two files. You have the raw folder that is going to hold all your source documents, articles, notes and images untouched but your source of truth you can say. Then you have your wiki folder that will be generated and that is a fully large language model generated markdown file and it includes summaries, entities and different sorts of interlin concept pages that your large language model can reference any single time and it is actually going to be something that constantly updates, maintains and cross references whenever it needs.

**7:18** · Essentially, Cloud Code is going to set up any necessary scripts or tools that you can ingest new data for, ask questions, and have the wiki self-improve automatically with this new system.

**7:31** · So when I was working with claude code to set up my vault with this new wiki or this new gist that Kaparthi or Arpathy had developed, I essentially had described it so that it is going to be able to work with front-end designs, UI inspirations, and landing page examples.

**7:50** · This is where within the raw file, I'm going to be providing multiple assets for my cloud code agents to actually use. This is where I can add screenshots, Figma links, HTML, CSS snippets, notes on colors, fonts, any design system that I really like for my development. This is something that will instruct my coding agents to follow through with this in-built memory so that it doesn't hallucinate and doesn't generate anything else. So these are the two different folders that I have created with different subfolders that will be self-updated with the design library where cloud code or other agents can pull relevant information and generate new design ideas whenever it's needed. So for example, if there is a new package or documentation that you want your large model to reference, this is just an example. What I can use is the new extension that I had just installed which is the Obsidian web clipper. I can essentially add it exactly to whatever file that I want.

### Frontend Example

**8:49** · And this is where if I to click add to Obsidian, it is going to be able to then open up Obsidian and then provide that raw markdown format. Exactly. And you can see that it does a great job downloading the related images locally so the large English model can see them.

**9:04** · It can drop everything into the RAW file which you see over here. And what you can even do is tell your large English model to compile the new raw files into the wiki. create summaries, extract concepts, and even add back links to update the index MD. So, this is what I'm going to be doing. I can now go back into my Cloud Code instance, and I can tell it to compile the new raw files into the wiki. And now, what I can do is head over to the index file. And this is something that my agents can now cross reference for whatever features that I have set within my vault which is primarily focused on front-end development to help cloud code better generate frontends. Now this is super simple guys. You just provide your raw files. Then you simply ingest it into your index MD so that all the raw material plus the clean large signage model generated wiks can be stored properly for our AI coding agent to reference any single time. And this is going to make your AI agent perform better because it has the ability to reference all of these interlin sources that it can use any of them any time. It turns any scattered notes that you have within your raw files into a connected personal knowledge base that Claude can read and reason over making its coding and answering much smarter and more accurate. And something to note is that within your Obsidian vault, you have a graph view which will better understand and visualize all of the elements a part of your structured database. So, what I can actually do now is have it work upon creating something like a dashboard, a CRM dashboard that's able to reference the index MD to better implement the charts and UI components that I had referenced. And this works really well when you have a lot of data that you want your large models to perform. And you all know enthropic models, Gemini models, all of these models are lazy and they're not able to perform at the best capability until you prompt it properly.

**11:06** · But then again, even with prompting, there is a lot of occurrence of hallucination, which is why you need to have these different memory systems instilled so that it is going to be able to complete the generation better. And there we go. Just like that, it was able to reference and use all of the different components that we had provided within our raw index. And this is essentially where we have all these cross-link references to all the different charts from Shhatzien that have been implemented into our app, which is incredible. You can see that over here. And this is why this is such an incredible tool because I'm able to save a lot more on token expenditure because I am working on scraping the content for the large language model to actually use. Also, the fact that it is going to save a lot of time in understanding and specializing on what to use and when to use for any sort of use case. And the fact that I did it quite quickly for this is incredible.

### Output

**12:05** · Remember guys, the self-improving part is the most important thing about this because it actively gets better as you use it periodically because once you run the lint command or the health check command, you can simply run a prompt that is stated within the wiki, which is to review the entire wiki for contradictions, still info, missing links, or new connections and fix and improve it. This is something that I'll also leave in the description below, but essentially the large language model reads its own previous work, spots gaps, resolves issues, adds better summaries, and makes everything richer and more connected over time. So that whenever your large dangage model is using this information, it is going to be able to self-heal the knowledge base that keeps getting smarter with no manual editing needed. So the more you feed it the and lint it, the better claude becomes or whatever AI coding agent you link to it and it's going to answer your questions and write code better based off of that raw data that you provide it. So essentially you want to provide as much data as you can and lint every single time whenever it's possible. If you like this video and would love to support the channel, you can consider donating to my channel through the super thanks option below. Or you can consider joining our private Discord where you can access multiple subscriptions to different AI tools for free on a monthly basis, plus daily AI news and exclusive content, plus a lot more. But that's about it, guys. This is something that will turn any AI coding agent better at answering your questions and writing code. and it's something that I highly recommend that you take a look at with the links in the description below. Huge props to Andre for developing such a great system. Make sure you go ahead and take a look at our second channel. This is where we're constantly posting AI news on a daily basis. Join the newsletter, join the Discord, follow me on Twitter, and lastly, make sure you guys subscribe, turn on notification bell, like this video, and please take a look at our previous videos so that you can stay up to date with the latest AI news.

### Enable Self-Eolving

**14:04** · But with that thought, guys, have an amazing day, spread positivity, and I'll see you guys really shortly. He suffers.