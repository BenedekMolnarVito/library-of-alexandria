---
title: "OpenClaw......RIGHT NOW??? (it's not what you think)"
source: "https://www.youtube.com/watch?v=T-HZHO_PQPY"
author:
  - "[[NetworkChuck]]"
published: 2026-03-30
created: 2026-04-18
description: "Get your own VPS and set up OpenClaw: https://hostinger.com/ncopenclaw Use code NETWORKCHUCK!OpenClaw has 308K GitHub stars — more than React, more than the ..."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=T-HZHO_PQPY)

## Transcript

### OpenClaw stressed me out (308K GitHub stars)

**0:00** · Okay, here we go. Open Claw. We're going to need two copies for this.

**0:07** · This software is the reason AI has been stressing me out so much. See this video here, but you can't ignore it even though I want to, even though I kind of hate it. It's here. Currently, it has 308,000 GitHub stars, beating React and the Linux kernel somehow. The creator got aqua-hired by OpenAI, \[music\] and everyone's copying it. Just last week, Anthropic dropped channels and dispatch. So, that begs the question, do we even need Open Claw? Am I using Open Claw? Short answer, yes. I've been using it since it first came out. I've got seven agents running.

**0:37** · And I've been talking to Peter, the creator of Open Claw, before it was even called Open Claw. I actually helped him with the rebrand. But, I also kind of hate it, and it's not what you think it is. And yeah, I know I'm late to the party here.

**0:48** · I actually recorded this video twice.

**0:50** · Stuff keeps happening. I'm stressed.

**0:54** · But, you have to admit, it's pretty cool. Put the hype aside, look at this. Remember when we built our news aggregator inside in 8n? A bunch of nodes, a bunch of hours. It was cool, but then Open Claw can one-shot this in one sentence. Same thing for our IT engineer. We spent a lot of time building that inside in 8n.

**1:11** · Open Claw crushes it in seconds. So, my goal for this video is to put the hype aside and really answer the question, should you care about this? And normally, I would say by the end of this video, you're going to have your very own Open Claw agent set up. No. I'm going to break a YouTube rule right now.

**1:24** · I'm going to walk you through setting it up right now, at the beginning, because I think it's one of those things where you just have to try it. Like, get it set up and have it do \[music\] something.

**1:33** · It'll take 5 minutes. Get your coffee ready. I'm going to pour some more coffee, boss.

**1:38** · Let's think and go.

### Setting up OpenClaw in 5 minutes on a VPS

**1:44** · 5 minutes on the clock. We're going to get you set up with Open Claw fast. I'm not sure I can do that, but we're going to try. Now, what do you need? You don't need a Mac mini, even though it is pretty cool and I tried it, it's fun.

**1:53** · But, you do need somewhere to install the Open Claw gateway. This somewhere can really be anywhere. I'm going to show you in the cloud, inside of VPS on Hostinger. They are the sponsor of this video, and the sponsor of getting you spun up as quickly as possible. And I'm not sure why I'm making a list. That's really pretty much all you need, and some coffee. \[music\] Need some coffee.

**2:10** · Cuz everything in IT requires coffee.

**2:12** · You guys know that, right? So, head out to hostinger.com/ncopenclaw.

**2:16** · Now, you would think we might click on the one-click setup, because it's faster. No, we're not going to do that.

**2:20** · Instead, we'll go to services, \[music\] click on VPS hosting, choose KVM 2 because it's an entire home lab in the cloud, put in coupon code NetworkChuck and watch magic happen, and your VPS is brewing. I'm going to have another cup of coffee here.

**2:33** · Mhm. And boom, you got a server. And by the way, this isn't just for Open Claw, it's for whatever you want to do. You'll see. Once your server is done brewing, we're going to grab that SSH command.

**2:42** · Just copy it, launch your favorite terminal, paste that command, and \[music\] we're in.

**2:48** · Now, time to install Open Claw. This is the easy part. Now, documentation does change, so we're going to go straight to the source, openclaw.ai. Scroll through all the lies. I'm just kidding. Until we see this one-liner to install it. Copy that. Get back to your terminal.

**3:01** · Paste that one-line command, and that's pretty much it. Hit enter, and relax. One more sip of coffee.

**3:08** · And it's done. Now, scroll right past that security warning. We don't care about that right now. We'll talk about it later, don't worry. Hit yes, I understand. Let's do a quick start, and we're here with our first option. Which AI model are we going to use? Because guess what? You may not have known this, but Open Claw is not itself an AI. It's a harness. It's a layer sitting on top of other AI. So, right now, we're going to choose what brain it has. Now, I love this because this is the open part of Open Claw. It doesn't care what you choose. You can even go local models.

**3:34** · Ollama is even now officially supported.

**3:36** · But, you're going to have a better time with OpenAI or Anthropic. I would choose OpenAI because Peter works there, and Anthropic's kind of being a jerk right now. But, I still love them. Now, what's really great about this is you can either go API key, which is pay as you go, or if you already pay for ChatGPT Pro or anything higher than that, use that. Use your subscription you already have. So, select that first option. And you got to do this weird off thing, so we're going to grab this URL. Copy that.

**3:59** · Open up your web browser. Paste that URL in. Log in to your ChatGPT account.

**4:04** · And then, don't let that message scare you. Just grab your URL. Copy that from your URL bar. Get back to your terminal.

**4:10** · Paste that in there, the redirect URL, the one you just copied. Hit enter. Go with the default model, 5.4, can't beat it. And now, we're hitting something that makes Open Claw kind of awesome.

**4:20** · And that's how you talk to it. Pick which you want, but we're going to start with Telegram. It's very easy. Now, we need to create a Telegram bot and get our bot token. For this, we'll launch Telegram. You'll start a chat with a guy named The Botfather. This kind of feels like a video game. You'll create a new bot, name your bot, give it a username.

### Connecting Telegram and hatching your agent

**4:36** · It must end in bot. Create that bot. And that's it. Click on copy, and that gets you your bot token. Get back to your terminal. Hit enter to enter your Telegram bot token. Paste that in. Hit enter. Hey, this is actually new. I've never seen this. We'll go with Brave.

**4:51** · Ah, we need an API key. I just hit enter to skip it. Configure skills now? Uh, not right now. Hit no.

**4:57** · And for hooks, go ahead and do hooks.

**4:59** · Enable boot, bootstrap, command logger, and session memory. Hit enter, and that's pretty much it. Now, it's time to hatch your Open Claw agent. We could do the web UI, but come on. We're going to do the TUI. Select TUI, the terminal user interface. Hit enter, and we're waking up our friend. Again, this kind of feels like a Pokémon game or something, like Pokecopia. Yes, I played it. It's pretty fun. Now, this is what makes Open Claw feel kind of weird. And what's interesting is when you configure Open Claw, this is it.

**5:29** · Like, you're talking to it to configure it itself. So, we'll tell it who it is, who we are, and get started. You're Terry Crews. You are NetworkChuck fan.

**5:38** · You're chaotic. Muscles emoji.

**5:41** · Now, what's really creepy about this is that all of this written right here was written to his soul.md file.

**5:47** · His soul.

**5:49** · \[sighs and gasps\] Now, enough talking in the terminal. That's cool, we like that. But, Telegram awaits. Let's go to Telegram real quick.

**5:55** · Let's click on our Terry 3 bot. And let's start a conversation. Let's message him. Start. And this is one of the security features I like. Not just anyone can talk to Terry 3.0 out the gate. We have to sync it up. So, I'll just take this. This will be your first experience configuring Open Claw with Open Claw. We're just going to copy all this mess and say, "Hey, continue configuring Telegram for me. I'm lazy."

**6:17** · Paste that in.

**6:18** · Take a sip of coffee. Done. Ignore that security risk stuff. We don't care about that right now. But now, in theory, I could say, "Hey, you there?" Terry's typing.

**6:32** · And he's here, talking in Telegram. And timer done. Did we do it? I don't think we did. But right now, you have Open Claw set up. The killer part about this is I can now get up, walk away from my computer, have Telegram on my phone, and just talk to Terry.

**6:47** · One thing you just did though, and I can't believe you did this. I can't believe you fell for it. You just configured Open Claw, one of the most insecure things out there. Prompt injection, malware hidden in the skills.

**6:59** · You're a walking, talking CVE. And now, I'll do that YouTube thing. Later in this video, I'll show you how to add some security features to get you to where you're not scared. I get it. If you want to go ahead and jump there, go ahead and do it. But before you do, let's actually do something with our Open Claw. People say, "Oh, it's just an assistant. What's How is it useful?" And I get that. I live that sometimes. But let's do something to make you go, "Oh, okay." And that way, you walk away from this video with something cool.

**7:24** · Even if you don't do anything else with it, this is going to be awesome. Step one, news briefing, or project one. Now, \[laughter\] remember in 8n, this took us forever. This was a whole video teaching you in 8n, how to use the nodes, how to program it, Python, all kinds of stuff. Watch this. I'm just going to tell it, "Hey, I want to see some news.

### Project 1: AI news briefing (one sentence vs entire n8n workflow)

**7:41** · Cybersecurity, you know who I am, NetworkChuck. You know what I'm into. Give me YouTube videos, scrape Reddit, check Hacker News. And don't just give me stuff. Tell me if it's worth my time to read it or watch it. Rate it for me."

**7:52** · We tried \[snorts\] to do that with in 8n, it took forever. Ready, set, go, and Terry just does it for me. Done. Let's make it a dashboard. Let's have him make one right now, after you put him in high thinking mode. Let's do the same for us right now. That took a minute, but it's done. Let's check it out. It gave me the DNS name.

**8:07** · That's sick. And that's actually pretty cool. It told me I should maybe watch this video from David Bombal. Let's go see. Project one was super hard. Project two, let's turn Terry 3.0 into an IT engineer. Let's have him monitor his own server, the one he's on. We'll do {forward slash} new to give him new context. We'll make him think hard.

### Project 2: AI IT engineer monitoring your own server

**8:26** · And I'll tell him to become an IT engineer. You're an IT engineer. Your first job is to monitor the server you're on. Check everything. Internet speed, RAM, CPU, security logs, and create a dashboard for me. Go. And I love that. It's going to investigate its own box, make sure it doesn't step on any toes and break anything, and then build something. Okay? We're not getting hyped, but hype to the side.

**8:47** · It's pretty cool though. You have to admit it. I'm not saying turn it loose, but that's pretty cool. And it's done. It did the same kind of theme. But wow. I mean, this is pretty cool.

**8:59** · It's a one-shot. And yeah, it's updating live. If you did those two things, you have two real things to walk away with, and I'm hoping you're inspired just a little bit. Because what it just did here was I Come on. It's It's neat. And if you're anything like me, you have a bunch of ideas. Now, by the way, this is a just getting started with Open Claw video and my raw thoughts on it.

**9:19** · For a more structured setup scenario, and getting this set up properly, and diving deeper into things like security and memory, setting up Q&amp;A, we'll have a course on NetworkChuck Academy coming out soon, if not already out right now, so check the link below. But, let's step back for a second. What even is this? Like, what did we just install? What exactly is happening, and why did I let you let this loose on your VPS in the cloud? We got to secure that sucker. We'll do that here in a second.

### What IS OpenClaw actually? (gateway + 4 pillars)

**9:50** · Only had off-brand in the fridge.

**9:54** · So, real quick, we're going to talk about kind of what Open Claw actually is, why people are freaking out about it, and why you maybe should care about it or maybe shouldn't care about it because I I do use OpenClaw but not all the time and not for what you think I would use it for after seeing that demo. But anyways, OpenClaw it's simply a gateway. It's a gateway that connects a few things together.

**10:15** · Now, this gateway is just a service running on your computer. You want to see it? Type in PS AUX pipe and we'll grep for claw. There it is right there, the OpenClaw gateway. It's a node.js app just sitting there running 24/7. Now, this gateway connects a few things. Three pillars that make it kind of awesome but not exactly groundbreaking.

**10:35** · By the way, I'm doing this because I recorded it in a few different sessions and it got kind of messy, so I'm cleaning it up now. Now, back to me. First thing it did is it said, "Hey, whatever AI model you want to use, you can use that."

**10:46** · That's pretty sick. And then the killer feature was the channels. Most AI companies say, "Hey, if you want to talk to our AI, come to our platform. Come to us." OpenClaw is like, "No. Whatever you're using, we'll come to you. Telegram, Discord, Slack, we'll do it."

**11:00** · The third thing is the memory. You saw that as we were creating this, we were giving it a soul. And it has a bunch of mechanisms to start learning from your interactions. It starts to become and feel more like a personal assistant. It will remember the things you tell it. Now, you're probably thinking, "Chuck, ChatGPT does that. Uh Claude does that."

**11:19** · I hear you. This feels a bit different though, especially when you add on things like QMD or other fun memory things cuz I mean, this This is kind of your system. You control a lot of what's happening. Like that memory is going to live on that hosting your VPS you just set up. It's a markdown file. That's pretty cool.

**11:35** · Actually, let me show you where the files live. Let's get back into our server. All this might seem like magic but let me show you the stuff behind the scenes. Let me show you OpenClaw's house. First, we'll CD into our home directory where OpenClaw lives. CD tilde /.openclaw.

**11:51** · Type in LS. And that's all this is, directories, files, markdown files. And I think it does help to just get in here and see this because as you're making changes to Terry or whoever your agent is, it might feel like magic and you might feel like you're losing control. Like, I just told him to do something or told him to change his identity.

**12:08** · What just happened? You can see it happen. You're in control still. So, right now, most of what happens is actually in your workspace directory for your current agent. Let's jump in there.

**12:17** · CD workspace.

**12:19** · Type in LS. Couple cool things here. Your agent has a soul.md like we just talked about. Let's cat his soul. Cat soul. And honestly, this is a bit creepy. You're not a chatbot, you're becoming someone. And then what's really interesting is that we also have an identity file. So, Peter separates the identity from the soul. For humans, I agree. For chatbots, that's creepy. Let's take a look at it. Cat identity.

**12:39** · And this is more what we filled in with our first conversation. There's also a memory file. This is like Terry's long-term memory. Let's cat that. Cat memory.

**12:48** · And similar to you, this is stuff that is long-term that you really want to remember like your wife's birthday, your kids' favorite color, or all 150 Pokémon. Same kind of thing. Goes in the long-term. There's even a memory directory. If we CD into memory and we LS that, there's a file for each day like a journal, things that happened, conversations. Let's check the first day. Cat 2026 16. And I love this. Day one.

**13:12** · Woke up. Just knowing that this exist should make you feel a little bit better. Like, why did my entire IT infrastructure go down? Oh, let's check my agent's journal. See, we're okay. And if I were to chat with my agent and tell him to change something like, "Hey Terry, your favorite Pokémon is Gengar. This is a core memory. It defines who you are. Update soul and not soup. Update soul, identity, and memory, please.

**13:44** · Fun fact, Gengar is not my favorite Pokémon. Can you guess what it is?

**13:48** · Comment below. All right, let's see what he changed. Let's check \[snorts\] his soul. Gengar is core cannon. I mean, Gengar is core cannon. Identity. Favorite Pokémon, Gengar. Long-term memory. Favorite Pokémon's Gengar. Let's check his dear diary. Declared Gengar is Terry's favorite Pokémon. See See, it's not this mysterious box. It's not magic. Kind of It's kind of magic. But at least now you know how the magic is happening.

**14:13** · This is Hogwarts right now. You're getting schooled on what's happening.

**14:16** · Oh, there's one more markdown file I want to show you and that's the agents.md file. This is the one that actually makes it feel kind of magic and you'll see why. Like look Look what it's doing. We'll cat the agents file. And this tells it like how to wake up and do things. And it's pretty extensive. Like first run, bootstrap, that's your birth certificate. Before doing anything else, I get your soul and user file. Main session, look at your memory. And like I didn't know this, it won't load the long-term memory in group chats by default. That's helpful. We have redlines which we'll talk more about later with security. There's protocols for when to reach out and when to stay quiet.

**14:48** · At the end of the day, it's just a fancy prompt. And guess what? It's not tied to any provider. If you want to go tin foil hat and go all local, which I agree with, you just change the model. The memory stays the same. You just do a brain transplant. And I lied about three things. There's actually four things.

**15:04** · And this might be the coolest thing depending on how you look at it and which is why people were using Mac minis for this. And that's the tools available to this OpenClaw agent. You're installing OpenClaw on a machine and saying, "This is your machine. Here are the tools I'm allowing you to have." So, in our VPS example, we're saying this is your VPS. You can run bash scripts. You can use cron to schedule jobs. You can use heartbeats to remind yourself to do things for me. Hey, Chuck from the future here.

### Tools, cron jobs, and heartbeats

**15:31** · I feel like I didn't explain enough on this crons and heartbeats, so here it is. And this is what makes it feel alive. It's the heartbeats and the crons. Heartbeats make you feel alive. Just realized that. I will say that OpenClaw does this better than anyone else right now cuz Claude and everyone else is trying to copy. And you saw a bit of this in the agents file that I showed you earlier.

**15:54** · You can tell your agent, "Hey, check in every hour or so just to make sure I'm doing okay." Or with our news briefing, that would have been a cron.

**16:01** · News briefing every day, 6:00 a.m. It's setting up real cron jobs on your server and that's all it is. Like it does feel like magic but it's just a stinking scheduled task on your server. Genius for how simple that is. Let's actually watch this happen. Let's have Terry do something. Okay, I'm going to have Terry actually create a heartbeat. Let's do that right now. I'll say every 30 minutes remind me to drink coffee.

**16:26** · This should set up a heartbeat. And also I'll say every hour just pop in to say hi and see how I'm doing. Let's see if he made the cron for coffee. Let's see if it's in heartbeats or heartbeat.md. It should be there. No. Let's get back to the OpenClaw directory. CD dot dot and look in the cron directory. We'll cat those jobs.

**16:50** · Yeah, there it is. I wonder why he didn't set heartbeats. Oh, he made a smart choice. The cron to be better. We can also see the crons with OpenClaw. Cron, I think.

**16:59** · Oh, OpenClaw cron list. And yes, OpenClaw does have a pretty extensive CLI tool list. There it all is right there. Hey, quick afterthought transition. I want to show you a few things here on the skills, ClawHub skills, the browser access, and subagents. Here you go. OpenClaw also has skills which is both a good thing and a bad thing. They have a whole website called ClawHub. Let's go check it out. This is a directory of skills that just give your agent extra things it can do, skills. So, if I go to browse skills, you can see that there's over 33,000 skills. Please be careful.

### ClawHub skills, browser, and sub-agents

**17:31** · There's a lot of bad stuff in there. Lots of malware became a problem. Um let's find a simple one to install.

**17:36** · Let's give our agent some ability like the ability to make Microsoft Word documents. Perfect. You can see that they partnered with VirusTotal because again, there were problems. This is benign. We should be okay. Now, to install, we'll want to have actually ClawHub installed. So, we'll do npm {dash}i {dash}g clawhub to install ClawHub. And then we'll do clawhub install. What's it called again?

**17:59** · Word.docx. It's installed. Let's see if he has it. He sees it. Let's have him create a Word document. Let's have him create his own resume. Okay, he finished the document. Told me it's coffee time. Let's take a look at it. And there's Terry's resume.

**18:11** · \[laughter\] Four CCIEs.

**18:14** · I love it. Also a little creepy how good that is. I can also have Terry browse the web. Go to networkchuck.coffee in your web browser and tell me what you see. Yes, he does have a headless browser. Add default route to your cart. Added a product to its cart. You can also do subagents. Deploy a subagent to research the best way to make coffee.

**18:38** · Now, here in Telegram, you also have a lot of commands you can use. For example, I can do {forward slash} status. It's being queued right now but I can see everything that's going on right now including subagents active. I can do {forward slash} subagents list. It's extremely powerful. And that's just a subagent. You can actually install multiple agents like Terry under one gateway. I actually have that right now with my IT department. I have Ron as the the IT manager and then Fred, George, Charlie as individual IT employees, network engineer, storage engineer.

**19:09** · I can message them all in Slack. It's awesome. That's a video for another time, another episode in the series.

**19:16** · There's the results. AeroPress is actually a great thing. Actually, my daily grind is French press and then AeroPress when I'm camping and coffee boss when I'm in Japan. Now, is this groundbreaking?

### Why everyone freaked out (my honest take)

**19:27** · No.

**19:28** · No, it's not. A lot of this has already been done. And there's software out there that does some things better. What this did though, and this is the reason everyone freaked out, is it made everything seem accessible. It packaged everything together in one clean install and said, "Hey, look at this."

**19:44** · And it's suddenly like it was a collective light bulb around the internet. Everyone's like, "Oh, this AI thing, it can actually do if you give it the right tools. And of course the it's the idea of buying a Mac Mini and giving an AI control of it. Like this is the AI's computer and you're onboarding a new AI employee. Like that idea, that's what went viral. And it's great marketing because then you go, "Hey, I'm a human.

**20:10** · I use a computer. This AI can now use that same computer I use. Okay."

**20:15** · So, that for me, that's what I think happened there. But this tooling is not anything new. In fact, I think I think Open Claw is going to be around for a minute, but I see the bigger companies coming for it. Jensen Huang called Open Claw the operating system for personal AI. Nvidia built their own version called Nemo Claw, which apparently is very insecure. Anthropic's building theirs, I think. When the biggest companies in tech converge on the same idea, that's a big deal. And these companies aren't just going to buy into that without a certain level of security.

**20:44** · Whereas Open Claw's kind of like, um this is fun. Let's just deploy things without thinking about security, which is what kind of leads us into this next discussion. Oh my goodness, security with Open Claw. I can't believe you installed Open Claw.

### Securing your OpenClaw instance

**21:00** · I'm just kidding. It's not that bad. But let's get to it right now. And then I'll give you my verdict on is this hype? Is it cool? What How am I using it? Cuz I I am using it, but it's kind of like I'm Okay, I'll get to it. Let's talk about security real quick in this segment now. Okay, Open Claw security. Need some more coffee for this. I'm out of coffee. Oh, no.

**21:22** · Thankfully, it's gotten a lot better than it used to be. And honestly, you're probably pretty secure right now, but we're going to double-check. It was a dumpster fire to begin with, which is why we have a command like this. Run this right now. Open Claw security audit. When you run that, it's going to analyze your Open Claw instance and make sure that you're obeying security best practices. If you installed it like me, you probably only see two warnings, nothing critical, and we're probably good. You can do the switch {dash} {dash} deep to go deeper. We only had three warnings on that one. And you can do an Open Claw security audit {dash} {dash} fix for it to auto-fix anything that's broken.

**21:54** · Just be careful, it might auto-break things as well. Now, the big thing you want to look for is to make sure that your web UI is not exposed to the internet. Yes, you have a web UI. No, I haven't shown it to you. I don't really use that much. If you do want to access your web UI, I'll have a walk-through in the description below.

**22:08** · Actually, I did record something on the web UI. It's right here. To quickly test that, you can go to your public IP address and go to port 18789. If you can't access it, that means no one else can either. Because normally, when you install Open Claw now, it's tied to your loopback address of 127.0.0.1.

**22:26** · And all that means is that no one from the outside can access your Open Claw stuff, only things directly on your host. But to allow that, we can do what's called an SSH tunnel. We're not going to change any security settings, we're just going to allow us to access it very quickly right now with this command. I'll have it in the commands below, so don't worry. You don't have to memorize this. Or watch me type it in very quickly. Just make sure you put in your username and your IP address. So, we're going to paste the command in into a new window in our terminal, not the one we're logged in with at our server. Just like this. Put in your password.

**22:55** · And currently right now, I you're probably waiting for something to happen. Nothing's going to happen. Right now, you have an SSH tunnel to your computer. And if we open up our browser and we go to localhost So, what did we set the port to? I already forgot. Oh, 18789. We should hit that web UI for Open Claw. There it is.

**23:13** · Now, you may hit this where you need a gateway token to log in. And you're like, "Oh, Chuck, I don't have one. Oh, no." Don't worry, you have access to command line. You got whatever you got to do. Go back to your terminal, type in Open Claw config. This is a nice little TUI that'll take you through a few configurations. We'll choose local machine. We'll scroll down to gateway.

**23:32** · The port's fine. Loopback is good, don't change that. And then token, this is where we get our token from. And we'll generate it right now. There's my token. I'm going to grab that. So, I don't think it generated it fresh. I think that's my existing token. Although, it may be.

**23:45** · That token in.

**23:47** · Connect. And we're in. So, pretty much everything we talked about is in this nice web UI. You can chat with your agent here. You can view sessions, instances, channels. Channels are the Telegram, Discord, cron jobs. But don't you feel better that you're able to see it through command line? Yes, yes, you do. But honestly, from here, I mainly just talk to my agent. I rarely access the UI. And even the command line, I only use here and there just to make a few changes. Speaking of your host, we have to make sure that no one can access any other ports on your host. Is your firewall even enabled? Probably not.

**24:18** · Let's do that right now with this command. This command is going to enable your firewall and allow port 22 or SSH, which is how we're connecting to it with this terminal right now. We want everything else blocked except for the things that we need. Now, watch when I do this, I instantly lose access to the web servers that we built because it's blocking down everything. Let's allow that real quick, actually, because I still want to see my stuff. I'm going to allow port 8787. Actually, you know what? I'm going to have Terry do it.

**24:44** · Now, what's cool is that I need to approve this.

**24:47** · I'll allow it. And he did it. Actually, that's not cool. Having everything all the time kind of sucks. It is a security thing. Let me show you how to fix that right now. Let me show you how to make that happen and show you a bit of the confusing world of Open Claw security configuration. Now, I want you to run this one command in your terminal. Open Claw config get tools.dot profile. Now, right now mine says full and yours probably doesn't. It probably says coding. Why?

**25:13** · Because I got really \[laughter\] miffed and upset with the process halfway through this recording and I changed mine. Now, what does this mean?

**25:23** · It means if it's full, my Open Claw agent can see every tool on the system and it's available to it. It knows about it. Coding is limited and it can do things like read and write files, run terminal commands, but browsing and doing web search and any other tool that might be available, it like it can't see. So, if you want to change that right now, you want to make your agent more capable, let's do it. Keep in mind, this is a security risk. But there are ways around that and what most people do is a fully allow these tools and then they do what's called a redlining or redline. I don't know.

**25:53** · I don't know how the kids say it. But to change your profile to full, the command is Open Claw config set instead of get tools.dot profile. And set that bad boy to full. Hit enter.

**26:06** · And then you'll want to restart your gateway to apply that config, which is Open Claw gateway restart. You'll use this command a lot because Open Claw is open source and has updates like every day and things happen. Now, one more config that might mess you up, but I don't think by default, and it's this config here. Do Open Claw config get tools.dot exec. This config controls what Open Claw is allowed to do with the tools it knows about. So, if it's like you're like, "Here, here's a hammer, Open Claw, but you can't use it. You have to ask me first every time."

**26:37** · So, it's like, "Okay, I have a hammer. Can I use it?" That's kind of what's happening here, maybe.

**26:44** · \[laughter\] But not for me because right here, I have a very confusing security config called security full, which means he can fully do whatever he wants. It's not full security, it's I can fully do whatever I want. Whatever tool I know about, I can use it. Now, if you have the command set to allow list, then you can configure an allow list of tools your tool is allowed or your agent is allowed to use. I'll show you that file here in a moment. And the other option is deny. You don't trust your agent at all. Why do you even have one?

**27:11** · And then ask, you have the option for off, which I have. You might have that right now, which it'll never ask you.

**27:16** · So, right now, if you have this config combined with the tools.dot profile full, your guy can do whatever he fully wants. But you can also have ask to always, where it'll always ask if you're very paranoid, or only on miss, which combines with the allow list option. So, if the tool isn't on the allow list, then your agent can be configured to go, "Hey, I know I don't have a hammer on my list, but like, you know if I use it?"

**27:42** · That situation. Now, to change either of those two options, the command will be Open Claw config set tools.dot exec.dot security. And then whatever option you want to put in, like allow list or full. And then the same story as before, except we won't do dot security, we'll do dot ask. And sorry if you hear a kid screaming. My kids are right on the other side of that wall.

**28:04** · I'll just say ask off. Now, keep in mind, this is setting this globally forever for every session. You can configure these things per session in Telegram. I don't care about that. Now, real quick, to see the config, we can do cat openclaw.json, which will have a lot of the allow list stuff and security things in here if you love reading through configuration files. And we'll have a deeper dive video on security. But I'll go into my workspace folder and we'll cat the agents.md file, which is your agent's instructions, how it lives, what it does. You'll see a section for redlines.

**28:38** · Now, watching this back, I realized I kind of just jumped into redlines without explaining why this is here. Here's why. We just told your Open Claw agent it can do a ton of things. We took off its seatbelt. Now, with the redlining, we're telling it what it can and cannot do. So, yeah. Back to me. Like don't exfiltrate private data.

**28:56** · Don't run destructive commands without asking. When in doubt, ask. You might add additional things. Like don't ever modify SSH config. And that would be redline stuff like stop, ask me first.

**29:06** · You can do yellow line, which is do it, but log it. Like making firewall changes or running Docker commands. And then you have of course have always allow whatever you want to do. Keeping in mind that this is agent.md instructions, like a prompt that your agent should obey, but also it's just a prompt. There's nothing deterministic preventing it from doing it. Now, touching on security once more, be careful with skills and Claw Hub. 12% of skills were found with malware. I mean, ooh, be very careful.

**29:31** · Vet everything. Now, at this point, you don't have to freak out. Your gateway is not exposed, especially the UI is not exposed to the public internet. Only SSH is allowed. And right now, only you have the passwords, only you can log into this computer. And then we'll just actually verify one more thing. It should already be configured by default, but I can say, "Hey." And I'm talking to Terry right now.

**29:51** · "Make sure I'm the only one allowed to talk to you." You can allow others to talk to your agent if you want. I wouldn't do that. Security done. Now, let's talk about what I think about this. Open Claw is really fun. But, for serious work, I am normally going to be using Claude code.

### My verdict: how I actually use OpenClaw

**30:10** · And I'm normally sitting down at my computer and working with Claude code because I think it has a has better tooling and an overall better experience for things that I do, which is like research and scripting, a little bit of coding here and there.

**30:23** · But, I do use Open Claw. So, what I'll use it for? Number of things recently, actually. And this is kind of going to be an Open Claw series because I do think we need to unpack this a bit more.

**30:31** · One thing I did, and this is going to be an episode, is an entire IT team. And I have them right now. They're running my home lab and my my studio lab, which is my NAS and everything. I have a CTO and then an army, like an internet engineer, a a storage engineer, a systems engineer. It works pretty well. Like, I'm impressed. They solve problems. We have ticketing. I'll show you that.

**30:54** · Also, I do have a personal assistant that I rely on. Like, being here in Japan, it's been massive. Her name's Hermione because I'm a nerd. I have her do things like I Yeah, I let her check my email. And I taught her how to speak Japanese so she can actually make phone calls for me here in Japan in Japanese and make restaurant reservations for me.

**31:12** · That's kind of stuff you can do with that. I also just recently set up Arnold Schwarzenegger, personal training assistant for my health. He's going to help me lose weight, hopefully.

**31:20** · And get yolked. So, essentially, I have a bunch of very purpose-built agents I use. And I know I haven't fully unlocked the power because it's You have to spend a lot of time to think about that and figure it out. So, I'm kind of in dabble mode. But, it is cool. And I want to see what you can do with it. I want to see what the community can do with it. And I'm going to continue to tinker with it. I'm going to continue to play.

**31:40** · Which is why it's going to be a series. We're going to deep dive on security.

**31:43** · We're going to deep dive into other things we can do with like IT operations. As I mentioned earlier, Peter and I were talking about the rebrand before it was even Open Claw. I actually gave him crap on X when he renamed it to What was it? Multibot? And then he DM'd me asking for some help. We talked back and forth for a bit. And we actually had an interview lined up. Then OpenAI happened.

**32:02** · And I haven't heard from him in a while. Did you ghost me, Peter? Peter, if you're watching this, come on, dude. We got to do an episode here in this Open Claw series. In fact, everyone watching here right now, get your Open Claw, the the agent you just made, and have it text Peter in some way every hour until he responds to me and we do this interview. I'm like half joking about that.

**32:26** · So, Open Claw, the software that stressed me out. What do you think about it? Are you already using it? How are you using it? Or are you going to start using it after this video? Let me know. Is it all hype or does it actually meet the hype? Is it better? Comment below. That's all I got. I'll catch you guys next time.

**32:43** · Hey, you made it to the end of the video. And at the end of my videos, I like to pray for you, my audience. I believe in the power of prayer and what it can do for your life. And I do genuinely care about you. It's kind of weird, I know. But, let's let's pray.

**32:55** · Let's do it. God, I thank you for the person on the other side of the screen, this camera. I thank you that they are passionate and excited about technology. And, you know, maybe they are kind of losing that zeal and that excitement right now because of AI. I know I'm feeling that. So, I pray right now over them, Lord, that you would give them peace and excitement for AI in whatever form it is.

**33:21** · Uh remove the anxiety, let it melt off of them right now. Let them feel peace and give them hope for the future, Lord. I pray protection over their jobs and their careers both both as they're getting started in their career and as they're establishing um their their current role and as they're looking for promotions, God, just bless them in that, Lord. Go before them and make their path straight.

**33:47** · Give them clarity and give them direction to just wake up every day excited to work on the next thing.

**33:54** · Bless their families.

**33:55** · Um bless their finances. Let everything come into place. And I pray that as AI is kind of It is shaping the world, Lord. I I pray that their their identity wouldn't be found only in who they are uh as an employee or in what they contribute to their job or what their skills are, but their identity will be found ultimately in you, God. Cuz without that, we're going to end up lost.

**34:19** · And I know I find my identity in you, Jesus. And that's where my hope is found. So, whatever happens, no one knows what's going to happen, but you do, God. And if we find ourselves in you, we're not going to get lost. We thank you, Jesus, for everything. I thank you for this person and in this audience and this community. You have blessed us so much. It's in your name we pray. Amen.

**34:40** · That's all I got, guys. I'll catch you guys next time.