---
title: "Uber: Leading engineering through an agentic shift - The Pragmatic Summit"
source: "https://www.youtube.com/watch?v=i1tZN41VKcE"
author:
  - "[[The Pragmatic Engineer]]"
published: 2026-03-10
created: 2026-04-18
description: "With Ty Smith and Anshu Chada, Uber Dev Platform. At The Pragmatic Summit: www.pragmaticsummit.comUpdate on 11 March: the Uber team shared updated numbers as..."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=i1tZN41VKcE)

## Transcript

### Intro

**0:00** · Awesome.

**0:04** · Good afternoon, folks. Uh, thank you so much \[music\] for joining. I really appreciate it. Uh, yes, my name is Unshu. I lead the developer platform organization at Uber and Tai is a principal engineer. He's been one of the the leading engineering voices that's led our agentic shift, but also our overall AI strategy over the past couple years.

**0:25** · All right, let me try to get out of the way. Um, we have a pretty packed agenda, but I want to try to get to the end as fast as possible because I'm curious about your folks's perspective on what I'm going to talk about. Um, we're going to walk through what has motivated our push into Agentic AI um, and some of the key ROI that we we've uh, we've um, manifested. And there is key ROI. I'm really excited about the impact that that we've realized for Uber.

**0:50** · And then I'm going to hand off to Ty and he's going to get into the specifics, the actual technologies that we built or integrated that has resulted in that AI uh that impact. Uh and then I'm going to end the talk talking about some of the non-technical challenges that we've been dealing with organizational and cultural basically people challenges measurement and of course cost.

**1:15** · Okay. So um AI is not new to Uber. um our fairs platform, our matching platform has been using uh AI methodology for years and years. It's it's one of the things that sets us apart from the competitors. Um but over the past few years, using AI as part of the the engineering productivity and engineering life cycle, that's fairly new.

**1:36** · Um and it's AI's integration into not just engineering but all aspects of what Uber employees do has become uh a bigger and bigger part of what we want to focus on. So much so that DAR has stated that uh AI is one of our six strategic shifts. We move from a early from a human/ early AI powered company into a generative AI powered company.

**2:04** · Now I will say that that term is really p these days. Nowadays it's more fashionable to be an agentic powered company but the concept still holds where from the metrics from the data that that we've gathered um DA made this quote which is you know AI AI is enabling people to become superhumans um in terms of their productivity and the impact that we can realize for our end users. So from that standpoint, we want to enable all tasks that people do at Uber um to be supported by generative AI to augment human productivity.

**2:40** · And that last part is really important because um what we're not pushing for is AI automate all humans in in the company, right? And especially in the uh in the engineering side, what we found is we want to focus on enabling our engineers to focus on creative work rather than toil. I'm going to get into some of the metrics um and the impact that we realize from that.

**3:06** · the as we've unlocked AI, what we found is when we push some of the boring stuff to it, upgrades, migrations, bug fixes.

**3:18** · Um, not only does it result in much higher satisfaction from our engineers, they're able to push our product and create features for end users in ways that we didn't even thought was possible and at velocities that were have just been incredible. So, this has been the place that we've really been uh been doubling down on. Now one of the reasons we've been able to push on this is the capabilities of uh of the technology and the industry and part of it first part of it is we going from um pair programming to peer programming.

**3:49** · So if you think about back in the good old days of 2022 and 2023 uh when GitHub copilot first came out it was pretty uh novel way of augmenting development. You had a system where you could do synchronous tab completion, an ID chat window that would help developers move faster. And we saw it ourselves in our in our metrics. We saw about a maybe a 10 to 15% bump in overall diff velocity.

**4:18** · This is pretty phenomenal. But this by itself didn't push us in the direction that that we've seen over the past let's say year where the paradigm has shifted to peer programming where you could hand off workloads that are running asynchronously uh and the models that that we use are so good, they're so accurate that all you need to do with the AI agent is to redirect it in certain ways, maybe give it some some uh course correction.

**4:49** · Um, and that's that's uh all culminated in this model where we imagine developers acting as their own tech leads, right? Developers are are uh directing AI agents using a variety of the different models and capabilities that are available to be able to execute uh asynchronously and come back for for direction.

**5:09** · Now, this doesn't work for every single task, but again, when we think about some of the toil work that developers need to do, dead code cleanup, writing docs, library migrations, these all seem basic um these are basic operations, but they're absolutely essential for maintaining a healthy code base, but they don't by themselves help to grow the business.

**5:32** · So, pushing this workloads to AI agents in effect helps to grow the business.

**5:38** · Another thing that's really helped is the growth of the capabilities of the system. So on the right we see a uh logarithmic diagram that shows uh how long some of the models have been able to execute over the period of time. we go from, you know, less than one second to agents that can operate for hours and hours. And that's helped with this uh paradigm shift that's happened where again when Copilot was first introduced, it was still augmenting traditional development.

**6:05** · Um, but as the capabilities have gotten better, we've seen that this concept of vibe coding, which was just a joke a couple years ago, becoming much more prominent and much more of a serious concept. Um and it's resulted in companies like I have an example for ramp. I know they have a talk today. Um but there are other companies that have had similar examples. In fact, even Anthropic talked about how they were able to release uh co-work very quickly using a variety of agents.

### Toil automation

**6:32** · Uh this example is not unique, but it is representative of where the industry has been going so far.

**6:40** · Okay. So talking about toil um Tai's going to talk about the um the Agentic system that we've deployed out. As soon as we made our Agentic workflows available to developers, what we saw is 70% of the workloads that developers are pushing into the system were toil tasks.

**6:57** · There's a couple reasons for that. One is the accuracy of these tasks uh was much higher compared to the more ambiguous workloads. And it makes sense, right? like the start and end state of some of these tasks if you think about a library upgrade or a migration is much more straightforward versus say building a brand new feature or an experience out that requires an experiment because the accuracy was higher. Developers were more likely to push more workloads into the agent system that were toil oriented and it became a virtuous cycle that that we saw.

**7:28** · Uh and based on that, based on the success, we we uh pushed for making this as one of uh my org's developer platform's top priorities in terms of AI augmentation.

**7:41** · Okay, I'm going to hand off to Ty now to get into the specifics.

**7:44** · I'll start by saying that we are not building this in isolation at Uber. Uh Uber's had a long history of building AI solutions and having a lot of engineers across the organization building infrastructure. And so we really see ourselves as building on the shoulders of giants where you know we have our uh

**8:01** · our historic Michelangelo platform which has had uh some public content in the past that provides things like uh a model gateway so that we can proxy and talk to the main uh frontier models or host internal models traditional inference training platforms and all the other things you would expect in an ML platform that within the last couple years has really started to lean more into like the agentic side and the APIs that we're using to talk to you know, Open AI and and Anthropic and those folks.

### Uber’s agentic platform architecture overview

**8:29** · On top of that, we have a lot of the traditional infrastructure and context at Uber that we would want to take advantage of. Things like having access to our source code, our engineering documentation, uh, Jira tickets, Slack information, like these are all things that to have an effective agent have organizational memory, it needs to start to get access to. Um, one of the key ones that I'll dig a little more into in the later slides is our deployment of MCPs throughout Uber. Um on top of that we see a lot of industry agents.

**8:56** · We really take uh a perspective of trying to enable the latest and greatest for our engineers allowing them to experiment uh allowing them to have a uh a learning culture and use the best of class. So that means that there's a lot of clients that are coming in that folks are using and we use a lot of those to build specialized agents. This could be our background agent platform that we're going to be talking about, our uh test generation platform or many other kinds of internal ones.

**9:22** · And then at the at the top of that we have you know the engine engineering enablement uh phrase that's been going around the industry. It's you know measurements and cost control and education and everything else that you would expect.

**9:36** · So let's dig in a little bit to how we think about uh MCPS. This became a very popular uh piece of technology in the industry last year and we moved very quickly to make sure that this was uh deployed and secure for our engineers so that we could um make them as productive as possible. So we ended up putting a a tiger team together from across the company that came together and designed a strategy and built a uh central MCP gateway.

**10:03** · Um, this allows us to both to proxy external and internal MCPs from our service infrastructure and expose those in a consistent way to engineers that handles things like authorization, um, telemetry, logging, everything else that you might expect. We also provide a registry and a uh, a sandbox so that developers can come in, they can play with these MCPS, they can make sure that uh, it's going to do what they're expecting and that they can discover new ones.

**10:32** · Continuing on with that, we also have at Uber uh through our ML our Michelangelo platform built agent uh the ability to build agents with both SDKs and with no code solutions, building agent builders, the ability to visualize, have telemetry, do tracing, um that way as folks around the company are building some of these solutions that have access to uh the internal services, the data sets, we can reuse these in other systems.

**11:01** · This can be discoverable and that we can provide a registry that's then can be found by other engineers or uh non-engineering alike to to deploy these and they're deployed consistently in a lot of our environment. This can be uh from our uh devpod infrastructure which is our remote um dev environment local laptops uh through our background agent which is called minions. We're going to introduce that here in a minute or deploy these in production.

### The cross-functional tiger team

**11:31** · So we talked about the agents, the kind of registry there, the MCPs, the registry there, all the different uh agent clients that our engineers might be using, be it cloud code or or codecs or cursor. Uh, one thing that we recognized we needed to platformize pretty quickly was a central ability to uh, provision and configure and update

**11:52** · uh, the clients, the agent clients themselves, the ability to install and discover MCPs from the registry, configure those inside of the agent clients, uh, deploy standard configuration management so that people who are just new to the space are having more effective uh, prompts and uh, configurations right away and management in connection into our background. task infrastructure. Uh so we built this tool called AIFX. It's a CLI. Uh and it is the kind of the forefront of what developers are using to access our agent infrastructure.

**12:25** · So let's let's take a minute before I jump into our our specific product and think about the traditional developer workflow. If you looked at how people were spending time, a little bit in planning, probably a lot in code authorship historically and then a small amount in review and then typically they'd be in this edit run build run loop of editing their code, building it, doing the verification using some standard idees.

**12:51** · Now, of course, this has been changing significantly with the agentic world. And so, if we look at what the the first agent workflow looked like, it might look something like this. you have a developer who's in the middle of using cursor or clawed code. They're uh giving a prompt. It's asking for the ability to proceed and approve commands and they're very interactive in the loop trying to drive it to an outcome that they want.

**13:14** · Um but what we're seeing emerge now uh in the industry and at Uber is both background agents that are running fully autonomously as well as the ability for uh multiple of these to be run at once. Right? This gets into this place where as an engineer, you're giving a prompt.

**13:32** · You're waiting for something uh to you're waiting for some time while it's running. You're thinking, "Oh, what am I going to do? Am I going to go have a coffee or browse Reddit? Uh, might as well kick off another background agent."

**13:42** · Uh, and so they get into this mode of the the new flow looks like running several agents at once, right? Um, this this sounds great. um we're I think us and a lot of the industry is trying to to push towards this but a lot of challenges start to emerge with this different way of working. One of them for us was we wanted these background agents to be running autonomous autonomously and looking at the external vendors that were offering you know tools like like cursor and cloud code and codecs all of them were running their background agents in other people's infrastructure.

**14:14** · And while we can get there, while that may make sense longterm, having the ability to bootstrap on our own infrastructure was really important to us and allowed us to move really quickly. And so we built a product called Minion. Minion is our uh formal background agent platform. It's built on top of state-of-the-art agents, CLI, and SDKs. Uh this leverages all of Uber's existing infrastructure. It runs in our CI platform. This has our monor repos uh checked out, ready to work in quickly.

**14:45** · Handles all of the network access into the rest of the infra. Um allows the connection to all of those MCP servers that we talked about earlier through AIFX.

**14:55** · Um it's integrated for the developer in a bunch of different work workflows and uh panes of glass. There's the web interface we're looking at here, which is one of the main um interaction paradigms, but it's also available through Slack, uh through GitHub PRs in the code review process, through the CLI that we saw earlier, and we have APIs exposed so that it can start to be uh connected to by other workflows and other services uh throughout the rest of Uber. And one other powerful thing is this offers good defaults.

**15:24** · So when people are coming here and kicking off these background jobs, you know, they're giving a prompt. They're expecting a PR out of this. They may not be giving the the ideal prompt or have the ideal setup for it. And we can provide great defaults for each of our monor repos, make sure that this is more likely to have a successful task that the engineer is authoring than if they um were, you know, if they just did this locally and they didn't have a lot of the u cloud MD setup or the other context that may want to provide.

**15:53** · So, let's walk through a demo real quick of what using Minions is like with an example. So, we have this web interface and in this this is one that I actually ran. We had a user report an error. Um, they said, "Hey, this is crashing on my machine when I run this command. Here's what the error is." And I threw that into into Minion.

**16:13** · I said, "Hey, you know, we we're having this issue. The user's on a Mac. Here's the error they're seeing. Um, here's here's the command that was run." And so, you can see a few things here that are cool. one, we have these existing templates that users can choose from that are well-written prompts that have uh placeholders they can fill in. Uh we have the ability to choose and run in our different monor repos. Uh it can run in both on a branch or we can switch it to a follow-up task of existing PRs or diffs. Uh we have all the task history here. We have some cool things here. We have uh I can select the agent.

**16:43** · So in this case, I'm going to run it in cloud code. Um put it out as a GitHub PR.

**16:48** · We've been in a long multi-year migration from Fabricator to GitHub. So having this dual mode is important for our internal engineers. And one interesting thing you'll see is this red icon here. What this indicates is that this wasn't a great quality prompt and it would have less chance of successful success. So one tool that we built into this was a prompt improver. The ability to analyze the prompt and make suggestions that the user can accept on how to have a more uh a higher chance of success.

**17:18** · Now once that kicks off, this is running, you know, background agents can take a little bit of time. We ping the users on Slack, uh give them links so that they can go ahead and track this.

**17:28** · And a few minutes later, uh in this case, it was 7 minutes later, the Slack notification pings them again. It says, "Hey, the minion task is done. You can go look at uh the PR here. You can go look at the artifacts."

**17:40** · So let's say let's not go to the PR quite yet. Let's jump back into the task completion. I have a view here now where I can uh see what ran. I can investigate the agent logs if I need to. If this failed, I can retry or have follow-up tasks. Let's say it failed. Then I can search through the logs here and start to try to understand what the agent was doing and maybe give a follow-up. But in this case, it it was successful. We got a PR out of that immediately. Um it was a very straightforward one. Uh our minion bot co-authors this with the person that kicked it off.

### Async multi-agent workflow model

**18:11** · Here we have a link Jira. We have the test plan of how it verified. Uh you can see it was authored here by which agent Claude was uh minion was running and it was a very straightforward fix that we got. So this was a very simple workflow. Um but it was very much easier for the developer to just hey dump in a prompt. Hey here's a problem the user is having and get a PR out of that as opposed to all of the context switching that they would need to traditionally do.

**18:41** · Right now the work the workflow for the developers has changed and is changing further. They're spending more and more time in planning and code review because there's so much more code being generated that they're being forced to do it. This probably isn't the favorite type of work that developers love doing code review. And there's a lot of challenges with that. If people are doing code review and it's taking more time, they're maybe slowing down. they maybe let more bugs in because they're missing it in review because there's much more.

**19:10** · So let's jump into a few of the investments we made to try to improve that.

**19:17** · So one of the big problems is context switching amongst all the background agents. This could be on PRs that are coming out or the agent itself needing attention. So we built a tool called code inbox which was designed to try to help with this situation. It's a unified inbox for PRs that a developer needs to review. And what's interesting about this is it's designed to try to remove noise. So only bringing out the actionable ones that are directly relevant for a user then when it needs attention, not when it's, you know, sitting there waiting for someone else.

**19:48** · And we put a lot of work into the smart assignments with code inbox so that we try to find the most relevant person to review the code both from a ownership and compliance perspective, but also the history of how that person was working uh their time zone. phone availability, their calendar availability. Um, and we we try to find the right person and assign and then have uh strict SLOs's that we track so they can see how long it's been assigned, help reassign, do automatic reassignment or escalation if necessary.

**20:16** · And then this it does a a smart job of the Slack notifications to devs. So, it's doing thing like batching notifications so they don't see uh a bunch of noise or accounting for their focus time so it's not bothering them in the middle of it or you know their um holiday time if they're out. Uh it'll also uh handle integrating this into teams existing processes. So, if teams have existing Slack usage with code review cues, uh we can plug directly into that and inject the reviews at at that level as well.

### Minion background agent platform

**20:49** · \[snorts\] Some of the other cool stuff that we built into this one was we tried to understand the risk of the change and we're going to continue to invest in that. Uh there's a much different risk profile to a small change in test versus a change that's in one of our key services. And so we we try to highlight that here by analyzing the surface area, the the blast, how much that's going to affect, what type of service that's hitting, um and then make those estimates so that we can raise that to the developer.

**21:15** · So they might put more scrutiny on the review or or bring in another person or you know whatever decision they might want to make for a riskier change.

**21:24** · So in the code review space I want to move on to a uh a second product. Uh this one we we talked about the notifications and bringing context awareness. Uh but this is our product uh it's called U review and this one is designed more at the review help itself.

**21:39** · There's a bunch of external products right now. We've all seen them in the market. everything from code rabbit to to graphite um all of those are are trying to solve this problem and we've played with a bunch and we'll continue to use external ones as well but what we found is we had a lot of internal context we had a lot of complexity like the migration between fabricator and github that made it make sense for us to have a platform that we were controlling

**22:04** · the surface area for the comments coming through uh and so what this work how this works is we have a pre-processor for the code and at that point we have a set of plugins that are going to run. There can be general defect bots that are analyzing it. Um, it can be pulling from best practices or MCPs or other types of information around the organization.

**22:22** · Uh, and we also have an API so that we can plug in external bots. So, if we were using, you know, one of those external code review tools, we can just plug it into the API here and have it surfaced with the rest of the comments that are coming in to the developer to help minimize duplicate comments or or extra noise. that then runs through a review grader. Um, this has been one of the co common problems that we've seen a lot of lowv value comments surface from those because they'd rather uh give something to the developer to do even if it isn't maybe necessary.

**22:51** · Uh, and we really only want to put the high confidence changes that the developer really needs to focus on, not little nits. And so this continues through the flow. It looks for duplicates from these different systems uh, and finally categorizes these. Now each one of these layers we've done evaluations and have different models running based on the uh the performance that each model has on the type of behavior.

**23:19** · This has been something we've been working on for most of last year. So we saw uh some growth uh and some progress in the system as as it matured. Um, one we saw that we were able to get higher quality comments uh at a higher rate as as we invested in integrated uh additional best practices and other rules.

**23:37** · Um, we also saw the rate of the comments and the best practices increase while maintaining a high rate of uh comments being addressed. uh this is the the specific piece of feedback that we're looking at to make sure um that this isn't noise that developers are actually fixing these and it's not uh just annoying them. And then here's a screenshot in fabricator not in GitHub where I mentioned we have to have the dual kind of UI uh because of the two systems at the moment.

**24:04** · Uh and so this was a a custom one we built to try to have a feedback loop for the developer in the code review space. it would it would uh wouldn't be complete if I didn't talk about the verification the validation CI test I think that's the other big part that we are really concerned about to make sure that the uh

**24:26** · those mistakes aren't slipping through code review as more code is coming in so we built a system called autocover that we've talked a little bit about in the past actually the author for it is uh I saw him around here somewhere um this this was a system that we designed to generate unit tests Now you might say, well you can just do that with cloud code or or many other products and you can but what we found is by really focusing on this project building a custom agent on top of our internal langx um SDK built on lang

**24:57** · chain we were able to get a much higher quality type of unit test output. Um, and so at this point we're seeing about 5,000 tests generated and merged per month around the company from this and um almost a 3x rate of quality versus something that would be generated from your typical generic agent. Now, as we were doing this, we were quite concerned with, you know, bad quality tests, change detector tests, things like that coming in. And uh, so we we built into this a critic engine. So it has both the generation and the critic engine.

**25:26** · And we separated that out into an independent test validator that now developers can use independently whether it's a human generated test or an AI generated test. Uh which is great to help uplevel uh the test quality in general and ignore any um false confidence that we might get from having the higher coverage. So I'm going to talk about one more category before I hand it back to Anu.

**25:49** · Uh we've talked about um you know authoring code initially and the code review process but code maintenance is a big area and you know at the beginning an was talking about the toil work. This is where a lot of folks kind of consider toil the heaviest.

**26:03** · So as we were looking at how to how to build this out, we we looked at the space. We looked at the messages coming out from other companies, you know, where their CEOs are going up in front of the news or to their their boards or their investors and saying x% of our code is generated by AI now. And we were looking at that and saying, well, how is how's some of this done? And some of the companies were very mature companies like like Google or Meta.

**26:27** · And we'd had a lot of discussions and seen that they had fundamentals that Uber hadn't invested before, which was the ability to kind of scale out large scale changes so that the AI can then build on top of that. And and so we got together last year and we decided we needed to run a big program to create a scalable version of how we handle large scale change. We called this automigrate. Um we broke this program up into kind of four key areas.

**26:53** · Uh we have the problem identification area where someone would be looking at a migration or an upgrade and deciding what the risk of the migration is or like what the surface area of the the change is or how to cut up the PRs so that they they make sense and drisk. You have the code transformer piece which could be an agent. You know we could be using uh you know cloud code or any others but it could be something deterministic like open rewrite which we've made a lot of investments with.

### Agent logs, observability, and debugging workflows

**27:17** · Then it gets into the validation phase where we need to understand how we get confidence that that automated change is going to be successful uh and that it's not just relying on human review. So this might be CI or unit test or sometimes even uh you know staging or production signal. Um but this is a key area as we think about it. And then finally um the the area of campaign management was something specifically that we needed to build from scratch.

**27:42** · you know, the ability if you have a 100 PRs that need to go out to developers for a migration, how do you get those all into the right spot? How do you track those? How do you make sure those folks are notified? How do you refresh this? And so this was this became the key of the platform that we called Shephard. Um here's introducing the experience with Shephard that the surface it's a web UI where developers can go, migration authors specifically, and they can track all of the PRs that are associated with a migration.

**28:12** · It will uh it allows them to define those simply through a YAML file where they can either give a prompt if it's an agent or they can point it to the script that's going to be handling it. And then Shephard is going to take care of generating those PRs, refreshing them on whatever cadence you defined, keeping those fresh for the developers, notifying the the people that need to review it, getting it in the right cues, integrating with code inbox, the last product I showed.

**28:36** · So let's walk through two quick um demos of this one. Here's a a PR using one of the deterministic transformers. This used open rewrite. Um we had Shepard uh generate all of the PRs to move our Java services to Java 21. Here we had this PR generated that um correctly found the owners created a limited PR in just the space of the code owners that upgrades it to Java 21. And we can see that generated here and a small change needed for that upgrade.

**29:07** · Here's one more where uh it's similar but in this case it's using the Minions platform. It's integrated with it as an agent. So we have separate tools in our programming systems group to do analysis, find performance issues. A lot of these are generating really great data. One of these uh we called um Dr.

**29:24** · Fix actually it's a different one. Sorry it's not Dr. Fix. Um, but it it identified these performance issues and it was able to generate a lot of PRs to and or diffs in this case to account for those, run those through Shephard, have a a standard thing that accounts for how how it was tested, how it was verified, what the developer needs to know to review it safely.

**29:46** · And with that, we've walked through kind of the major deep dive. I want to hand it back to Anu to talk about the couple last topics.

**29:53** · All right. Um, so Tai talked through a lot of the engineering investments that we made to make um, you know, the the agentic shift. Uh, I'm going to talk through a few um, non-technical challenges that we're still dealing with. First up is uh, on the people side um, and the business side. So on the business side um, I have a diagram here that uh, it's very topical since the Olympics are on right now. um the the leaders when it comes to AI tech is are changing pretty frequently.

**30:22** · Um you know the the models that are the most powerful for certain tasks whether you should build something inhouse versus use a SAS provider. These uh these decisions need to be re revisited on a pretty regular basis. Unfortunately, in a large organization like ours, some of the investments that Tai talked about, whether it's autocover, auto migrate, these are not trivial decisions to make.

**30:48** · We need to commit dozens of people on projects that might uh be running for months. So, we can't just change our mind after a quarter. \[snorts\] Uh there's there's two things that that we've done to mitigate this. One is seemingly pretty basic, making sure that we have the right abstraction layers in place. We talked about the Tai showed the the minions infrastructure under the covers. If we need to swap out the model or we need to swap out the technology that we're using, we're we're now able to do so.

**31:15** · Uh if if a better technology comes around that can solve some of the underlying um pieces more effectively, we can do so. Um but the the second part is just having this um this uh this belief that the tech we're building um will likely be replaced with something better in the industry.

### AI code review pipeline and quality grading

**31:36** · And so uh it's really important for us to not be married to the tech that we're building and being okay if something comes along like if the the co-founder cursor talked about the uh the auto the test coverage system that uh that might be coming in a couple weeks. I'm really excited about that. It might make our auto uh auto cover infrastructure um obsolete and that's okay because at the end of the day we need to deliver impact for Uber.

**32:04** · The second part uh is another is a people problem. Um so a lot of the challenges that Tai alluded to it deals with like you know historic infrastructure that's been built out over the last 10 to 15 years at Uber. Um we have some really sophisticated code that we built out and then we have some really um I would say archaic code that uh you know very few people know about.

**32:29** · Getting that technology integrated into uh to places where AI can reach it is challenging. Just getting MCP endpoints set up to reach to different parts of our ecosystem has been a challenge.

**32:43** · Similarly the tech that Tai talked about like I've seen in action it's magic. I I ran a demo session with some of my VPs and in 24 minutes I had four VPs land code for the first time in years. Um it was it was a pretty amazing experience.

**32:56** · They were pretty satisfied by it too. Um but our adoption for this technology has been relatively slow. It's been slower than I've expected and it's part of it is because we're trying to have developers uh do something that they're so not used to. They're used to looking at code and generating from scratch, operating in their IDE, and we're telling them to take a risk by operating in a very different way. In both of these cases, um, you know, we've tried different tactics to get around this people issue.

**33:24** · We've tried a top downs approach, you know, directives from leaders to say you must do X, Y, and Z, you must adopt. It's had some impact as we track, as you folks know, you track a metric, it's going to go up or it's going to improve. the more successful um uh technique that that we've applied is actually just sharing wins. So as we share examples between different engineers uh cool things that they've tried that have resulted in in wins, adoption of that technology has uh has erupted.

**33:56** · Um, so that's been the the tactic that we're we're pushing on now is key promoters pushing techniques to their peers because those promoters are typically engineers and engineers trust other engineers as opposed to directors like me.

**34:13** · Okay. Uh, I'm going to touch on uh measurements now. So um, we have tons and tons and tons of metrics. Uh, I can say with confidence that objectively AI is having positive impact. Um, our net promoter score, our overall developer experience at Uber has never been higher. Um, the the self-reported net satisfaction developers have and their productivity has never been higher. The amount of code that we're landing through AI is is amazing. The overall engineering velocity is fantastic.

**34:43** · And you can see the graph over here. we see the inflection point where when we were introduced agentic um the minions agentic system along with when the models became really really good like sonnet and opus being introduced uh the the delta between developers that are using it very casually versus the ones that are the the the power users that are using at least 20 days a week it's only exploded uh it's only the uh deviation has only gone up so uh I'm

**35:14** · really pleased about this now the the issue is that these are activity metrics, right? These are not necessarily business outcomes. And when we start talking about the costs of this technology, you know, our CFO has has asked me what is the impact of this, right? He I can't point him to diffs. I need to show him what's the impact on on revenue. Um I'm sure you folks are dealing with the same problem. We this is not necessarily a solved problem for us.

**35:40** · One of the tactics that we're taking this year is to instrument our uh overall feature infrastructure so that we can uh time from when a you know a design is first created to when an experiment is is launched in production and then seeing how we're able to speed that uh pipeline up. And then speaking of costs, the cost of AI is too damn high.

**36:07** · um you know since 2024 our our costs have gone up at least 6x. Now, I will say this technology is amazing. Like there's again no question that it's had positive impact, but it's gone from something that I can self-und using my own budget to something that I need to ask permission from, you know, the CFO.

**36:25** · What that's necessitated, especially where we went from a model where, you know, it's it's not necessarily cursors or Entropics's fault that it's going up.

**36:32** · The GPU costs are high and memory costs are really high. So we've had to be more responsible about how we use tokens, how we think about what's the right model for the job and then helping developers select those models. So again going back to the the example with minions, we help developers think about um the right model to form the plan for the uh for the project and then lower cost but still pretty effective models to do the execution.

### Testing

**37:01** · uh we don't necessarily want developers to think about it but we want to be able to help them uh help have the infrastructure decide for them so that we reduce the friction for them but then we also optimize our costs um but this is this is something that we continuously have to keep on evaluating and adjusting um especially as new technologies introduced so like this year we introduced uh Jet Brains AI and um and warp which we hadn't introduced in the past all have their own costing model and all about their own complexities with regards to how developers are using it.