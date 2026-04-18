---
title: "From IDEs to AI Agents with Steve Yegge"
source: "https://www.youtube.com/watch?v=aFsAOu2bgFk"
author:
  - "[[The Pragmatic Engineer]]"
published: 2026-03-11
created: 2026-04-18
description: "Steve Yegge has spent decades writing software and thinking about how the craft evolves. From his early years at Amazon and Google, to his influential blog p..."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=aFsAOu2bgFk)

## Transcript

### Intro

**0:00** · Tell me about your levels.

**0:01** · Level one, no AI. Level two, it's the yes or no. Can I do this thing in your IDE? At level six, you're bored because your agent's busy.

**0:08** · What is Gas Town?

**0:09** · If chat is complet, well, then we're going to put agents in a loop and that'll be an orchestrator.

**0:15** · That's all it is. It's agents running agents. There's a vampiric effect happening with AI where it gets you excited and you work really, really hard. I find myself napping during the day, but I'm talking to friends at startups and they're finding themselves napping during the day. We're still not seeing that much more output from companies, teams that you would expect.

**0:33** · What if what we're actually observing is that innovation at large companies is now dead. So I think what's happening is Steve Yagi has been a software engineer for 40 \[music\] years. He spent decades at Amazon and Google, is famous for his brutally honest rant about the industry, and for being right a lot. He recently built Gast Town, an open source AI agent orchestrator, \[music\] and co-authored the book Vibe Coding with Jean Kim.

**0:57** · In today's conversation, we discuss Steve's eight levels of AI adoption for engineers \[music\] from no AI to running multiple agents in parallel, and why 70% of engineers are still stuck at the bottom levels, why AI is creating a vampire burnout effect on developers, where you can be 100 times more productive, but only get three good hours \[music\] a day. his prediction that big tech companies are quietly dying and that small teams of 2 to 20 people will rival their output \[music\] and many more.

**1:24** · If you want to understand what the day-to-day of software engineering look like in the near future and how not to get left behind, this episode is for you. This episode is presented by Statsig, the unified platform for flags, analytics experiments, and more. Check out the show notes to learn more about them and our other season sponsors, Sonar and Work OS.

### Steve’s latest projects

**1:43** · So, Steve, really good to have you on the podcast again. What have you been up to, Ger? Great to be back. It's been uh 10 months now.

**1:53** · Closer to a year. Yeah, close to a year. Yeah, boy.

**1:56** · Seems like forever.

**1:57** · Yeah, sure does. Um uh yeah, uh it's there's been a lot going on. Um I'm uh unemployed right now, which has been incredibly fun.

**2:06** · Unemployed or funemployed?

**2:08** · I am um just doing whatever I want is what I'm doing, which is real nice. And uh had a couple software launches, which was nice. I had a book launch last year which was nice. I uh been living life.

**2:20** · Yeah.

**2:20** · So for a very long time you've been known as this kind of trutht teller of bringing in sometimes comical sometimes really uncomfortable facts or observations should I say. You wrote like often in really kind of fun fun ways with rants and a lot of them resonated with people. Do you remember what was around that really stood out and at any point in time that like you you got some really good feedback either at that point or later you felt validated by it?

### Important blog posts

**2:49** · Oh uh well um so a lot of people tell me well those who know their favorite Stevie blog is actually execution in the kingdom of nouns. I don't know if you remember that one. Way back in the day, I was at Google, early days Google, and I was uh trying I was struggling to sort of like get this idea across to people that Java's growth was super linear with the amount of code. So, the amount of code would grow more than the amount of functionality, which is not a good place to be. And uh Java's gotten a lot better since then, right?

**3:19** · But my post raised a lot of eyebrows at Sun because they were like, "What is this guy complaining about? Why doesn't he just shut up?" you know, but I was like, I want to use a language that has first class functions.

**3:29** · And so I wrote a very very very uh unusual blog post called Execution in the Kingdom of Nouns. People really loved it where it was a story. It was just a a fairy tale about a a land where there were no verbs and uh it was uh it was fun. So one of your lesserk known blog posts or for a lot of listeners, it's called a rich programmer food essay. rich programmer food. Yeah. And this was about compilers. Do you remember what you argued about or what the what points you made?

**3:58** · Of course. That's one of my most important blog posts ever. I got to tell you, I met a guy, okay, who he introduced himself at Swix's AI engineering conference in in in New York. And he's like, I've I've wanted to meet you, Steve. I'm one of your players, okay? And I'm like, whoa. Cuz this dude, you know, in his 30s, and you know, you know, he's played my game. You got to understand the game that I wrote.

**4:17** · It's something most people wyvern most people haven't seen it because I didn't open source it. I will someday. It's just a pain in the butt.

**4:23** · It's a really beautiful thing and it and it created so much love in the players for decades. They would come back, right? But this guy was so into it and he's like, I read your I read your rich programmer food blog post and decided to become a compiler expert. I became a PhD. He was in high school when he read it. Became a PhD. Started his own company. He's got a startup that's doing really, really well now. And he said it was all because of that post. And and this post talks about I think you argued that unless you know how compilers work, you're not going to be a good programmer, an efficient programmer.

### Shifts in what engineers need to know

**4:54** · I'm not sure what what the phrase was.

**4:57** · There's going to be a layer of magic between what you're doing and what the computer is doing that is forever going to be sort of a friction for you.

**5:07** · And then I think you even argued that some PhDs don't even understand how compilers work and this will make it really hard for them to be efficient. At the time that was definitely true, right?

**5:17** · How do you think that post has aged?

**5:19** · Because at that time I think it was like 2012 or so like even then I I would assume it was bit unconventional to say like you need to understand assembly because it was high level languages right Java was was was in its prime C Ruby was starting to come out I heck JavaScript was starting to become big react will start in a few years and most developers would have thought why would I need to know compilers assembly I mean that's what the compiler is for right yeah you're asking a really really really foundational question you're asking what universities should teach is what you're asking me, Gay. Okay.

**5:50** · In disguise and uh you know um that that those goalposts have moved every few years since I got into this game in the 80s. All right. What you need to know in order to be a software engineer, it used to be assembly language. It used to be like lots of bits and stuff like that.

**6:10** · And over time, my buddies and I realized that our favorite bit manipulation questions were starting to bounce off candidates who had never seen a bit before, right? And we \[snorts\] real, you know, we did some soularching in the 2010s, you know, and we were like, do you really need to know how to manipulate bits in a bite with XORS and stuff like that anymore? Probably not, right? And that was a depressing realization because we had prided ourselves in knowing how that stuff works, but we just don't need it anymore.

**6:37** · And the sad reality is that, and I I I had a lot of my own ego and identity wrapped up in my sort of compiler background. It's all it's interesting, right? But it's it's not useful in any meaningful sense anymore.

**6:50** · And is is it not useful because the compilers have gotten so good at optimizing for example? Is it that the problems have moved on to higher layers?

**7:01** · Why do you think that is walking up the abstraction ladder? That's all.

**7:04** · And we're not even talking about AI just yet. Like this this happened even say AI. Did you say?

**7:09** · No, not yet. We we will say it. Yeah, but but this but even in I remember like you know late 2010s it didn't really come up like in in my career I can only remember one time where it would have been nice to know what the compiler did but even then might have been a red herring honestly.

**7:24** · Look what you have to know just keeps moving. They just they keep changing the courses. They keep changing what they teach. Many people don't see this because they're only looking a year or two or three back and you know looking a little bit forward. But I've been doing this for 40 years and I can tell you they teach you very different things now than they used to teach. And it's because you need to know very different things. And nowhere is it more evident than when we saw the exponential curve of the graphics industry, computer graphics. Look at graphics today compared to 19, you know, 92 when I was learning graphics in university.

**7:51** · And I had to learn how to literally, you know, do the algorithm to figure out where the next pixel goes on a line so I can render it to eventually turn it into a triangle, which is a polygon. Meanwhile, two years later, I took the same course and we were doing animation.

**8:06** · I didn't even know what a polygon was. I mean I did but not at that level right the whole ladder just kept moving up and the jobs changed originally they needed people that could write device drivers and then they needed people and now they need people who can do game worlds and physics and all this stuff right it's they just graphics showed us the way this is what happens and software engineering jobs have been very stable for I don't know since iOS since mobile and cloud those are the last two big innovations right y Steve just made the point that the industry goes through these massive maturity leaps from raw pixels to game engines from bare metal to cloud.

**8:37** · And if you're building software today that needs to make that leap to enterprise grade, there's a tool that handles exactly that. This is our season sponsor, Work OS. If you're building any SAS, especially an AI product, authentication, permissions, security, and enterprise identity can quietly turn into a long-term investment. SL edge cases, directory sync, audit logs, and all the things enterprise customers expect. It's a lot of work to build these mission critical parts and then some more to maintain them. But you don't have to.

**9:07** · Work OS provides these building blocks as infrastructure so your team can stay focused on what actually makes your product unique. That's why companies like Entrophic, OpenAI, and Cursor already run on Work OS. Great engineers know what not to build. If identity is one of those things for you, visit work.com. With that, let's get back to the question of what the last real innovation in software engineering actually was.

**9:30** · And it's been kind of dead since then, actually. Yeah, I don't want to say AI because we're not talking about it yet, but but I think we went through a I think we went through a period where people stagnated a little bit where the courses didn't change very much and we thought this is all we're ever going to need to know.

**9:44** · I I I feel the last big innovation, correct me if I'm wrong, was distributed systems that that was the last kind of hard problem starting from like 2010s when you Uber brought brought microservices into there. How you scale services, how you store large amounts of data. I feel that was a like I mean it was a big it was a big slow yeah but honestly like I feel there's a

**10:05** · lot of migrations happening new react versions coming up and developers struggling with that Apple every year throwing in a you know like uh a screwdriver in in in the wheels with the new breaking version Android developers needing to retire an Android old version and deciding like where to cut it off.

**10:22** · So I feel there was that like kind of like migrations thing and and also business was just good right like everyone was growing we were like everyone was busy hiring like there's no tomorrow there there was a time in 2021 the market was so hot a lot of boot campers with 3 months experience we're getting offers a pretty good company cuz everyone was so desperate to hire and then came AI in in 2022 one thing that always struck me about you even in those like you know 2020s and even before you're always pretty pragmatic uh you know You were by by trade you were always into compilers, debugger tools.

### Steve’s current AI stance

**10:56** · That's where you started. You worked on hard problems at Amazon, at Google.

**10:59** · Never shied away to getting into like hard technical problems and you know like all all these things. And when AI came out, I don't remember you saying, "Oh, this is amazing. This is going to change the world." How did you feel?

**11:10** · Were you kind of like observing, skeptical like at the very beginning right when you first came across LMS?

**11:17** · How was that? I was pretty blown away that they could write fairly coherent Emacs list functions like like chatg the original one in in December 2023 2022 2022 okay boy time flies um could

**11:32** · already write code in a weird language right uh not very much of it and it was it was janky but that was for me that was the beginning of oh right uh you know because I've had friends in AI for 20 years saying any minute now any day now right and they'd show us and it complete better and better and better and this was the first time it was like oh okay I I see now right but I was still skeptical like everybody else and I can I can tell you because when when the rumors came out about cloud code in uh beginning of last year right that

**12:03** · anthropic had a tool internally that was writing code for them and it was a command line tool I I along with everyone else went no it's not you know it's we were just like just flatout rejection just absolutely not happening right until I used it and then I was like, "Oh, I get it. Uh, we're all doomed, \[laughter\] right?" And then I wrote Death of the Junior Developer right after that, actually. I think gosh, it might have even been after after uh 40 came out that I did Death the Junior Developer.

**12:28** · But things changed really fast once that came out. So, was I a skeptic? Yes. But did I pay attention to the curves from the very beginning? I figured if Chat GP35 can write a coherent emacless function, then in a year, let's see how they do. And in a year, 40 was writing a thousand lines of code. A thousand lines, dude, that's most of the world's code is in files of a thousand lines or less, which means that it can make credible edits. It wasn't able to up until 40 came out, right?

**12:56** · And so, like, man, it was that point when I was like, okay, we're on a curve. This is a ride.

**13:03** · It's not stopping. Let's get on the ride and see where it goes. And I dove in, right? And I was like, I was behind. I didn't know AI. I didn't know like the the fundamentals of I didn't know the lingo. You know, everybody knows this stuff now, right?

**13:16** · But I spent a year doing nothing but reading papers and catching up, right?

**13:20** · So in this book, Vibe Coding, I remember last time you were on the podcast, this book was about to come out and I was reading an early early version of it or so. But the back cover, I just read the back cover and I realized that you must have written this about a year ago and it says, "The days of co coding by hand are over." When did you realize this?

### Steve’s book Vibe Coding

**13:40** · because I've realized this, you know, recently with Opus 4.5, but this was this was a lot before well before that.

**13:47** · Mhm.

**13:47** · Yeah, it was a year ago. It was uh let's see, what is it right now?

**13:51** · January. So, it was over a year ago. It was 12 13 months ago when I first realized. And uh and it wasn't that wasn't even my quote. That was uh that was Dr. Eric Meyer, right? The inventor of many many many things uh in in the programming world, one of the most important compiler people in the world.

**14:08** · That dude, think about it. He spent his life building technology for developers to be able to write code and he's saying developers aren't going to write code anymore. What would possess somebody to say my life's work isn't really right?

**14:20** · And that's what caused actually Jean Kim and I both to go huh right you know if the inventor of you know you know he he made huge contributions to to to Visual Basic and C and and and link and and and Haskell and P and PHP with a pig. Is that what it's called? Right. All him.

**14:38** · And he's just like no we're done. We're done writing code. I mean, that's that's that's that's pretty big words from a languages person, one of the most famous in the world, right? What does he see that we didn't?

**14:47** · And he sees the curves, man. It's that simple. It's like exponential curves.

**14:53** · They get real steep real fast. And we're we're heading into the steep part this year. So, the inventor of C and Visual Basic is saying that we're done writing code. But even if the AI writes all the code, someone has to verify it. And that's where our season sponsor Sonar comes in. Sonar, the makers of Sonar Cube, has introduced the agentcentric development cycle framework, AC/DC, a new software development methodology designed for the unique scale and speed of AI generated code. It's a move towards a more intentional four-stage loop that gives agents the guards they actually need.

**15:24** · The four phases being guide. First, agents need to understand the canvas on which they're being asked to create so that the output fits with what the developer and organization require. Generate the LLM based tool generates the code it believes will achieve the desired outcome within the right context. Verify next. The agent is deliberately required to check its work, ensuring it actually achieves the desired outcomes and is reliable, maintainable, and secure. Solve.

**15:54** · Finally, any issues identified are provided to a code repair agent to fix. To power this, Sonar has significantly strengthened its offering, introducing products and capabilities like Sonar context augmentation, Sonar Cubagentic analysis, Sonar Cube architecture, and Sonar Cube remediation agent. Head to sonarsource.com/pragmatic to learn more about the latest with sonar and how it's empowering organizations to embrace the agentic era.

**16:18** · With this, let's get back to Steve's exponential curves of AI improvement. playing devil's advocate, you know, like one thing about being an engineer is like you you can draw up curves, but you know, like you never know when they end or if they flatten, what not. We can see where has come.

**16:34** · What made you believe that this curve would keep going and especially that with LLMs, the fact that it even kind of works was a bit of a I guess surprise for a lot of people and the fact that it kept scaling is a surprise and there's this question of like how long they will scale.

**16:48** · Yeah.

**16:48** · So, the world is filled with unbelievers.

**16:51** · Okay. people who specifically who believe the curve looks like this, an S. It goes up and then it flattens. Okay. And they actually think we're at the hump right now.

**16:59** · Yeah.

**17:00** · And they have thought that ever since the GP35 came out. They're like, "Yeah, it's not going to get any better." 40 comes out. We love 40. People love 40. They still do. They can't get rid of it.

**17:09** · But they still think that's as good as it gets. You know, Opus 4.5 is out and most people haven't played with it. Most people don't realize what's there. And that thing is already two months old. The half-life between model drops, as far as I can tell, has gone from about four months beginning of last year to two months from Anthropic at the beginning of this year. So any day we're going to see another model from Anthropic. It'll probably be out by the time we have this podcast out, right? And that will be so much further up the curve that people are going to start to be really freaked out by it.

**17:38** · It's going to it's going to worry people when they see the next model, okay?

**17:41** · because all of the bugs, all the mistakes that they're complaining about right now get fed right back in his training and so that it doesn't make them the next time. And this is what people aren't understanding, right? And also time continues. There will be three and five years from now. The sun's not going to stop, right? And it's coming.

**17:57** · So this inevitable the collision of these curves, man, it's there will be societal upheaval is what's going to happen. And it's already started. And people are justifiably mad. And I'm mad with them. Gay. Okay. I'm mad at Amazon for laying off 16,000 people and blaming AI without an AI strategy for it. Those people are not going to be able to find jobs by and large. And they're the first of many to come. And nobody has a plan for this.

**18:20** · Why? Wh Why do you think Amazon did that if they don't have an AI strategy?

### Layoffs and disruption in tech

**18:25** · Because um unfortunately, and people are going to hate me for saying this, but me saying it doesn't make it true. It was true already. Everybody has a dial that they get to turn from 0 to 100. and you can keep your hand off the dial, but it just has a default setting of what percentage of your engineers you need to get rid of in order to pay for the rest of them to have AI because they're all starting to spend their own salaries in tokens. And so, at least for a while, if you want your engineers to be as productive as possible, you're going to have to get rid of half of them to make the other half maximally productive.

**18:54** · And as it happens, half your engineers don't want to prompt anyway, and they're ready to quit. And so what's happening is everybody on average is setting that dial to about 50% and we're going to lose about half the engineers from big companies which is scary.

**19:10** · Yeah, that's wild. It's it's way that's way way bigger than we've seen back at co and it's going to be way bigger. It's going to be awful. It's but but at the same time something else is happening which is AI is enabling non-programmers to write code and it's also enabling engineers who have seen the light and believe the curves are going to continue to go up to actually get together in groups of two and five and 10 and 20 and 30 people and start to do things that rival the output of these big companies that are tripping over themselves.

**19:37** · And so we've got this mad rush of innovation coming up bottom up and we've got this mad knowledge workers falling out of the sky as the big companies lay them off because there's clearly the big company is not the right size anymore. It's not even Andy Jasse saying it. We're going to do the same thing with fewer people, right? And so does this mean we're going to have a million times more companies?

**19:58** · Is there going to be a massive explosion of software or people going to get out of software altogether and we're all going to go do other stuff? I mean like I I'm very curious where all this goes.

**20:06** · Yeah. small teams that have the right skill set or or see the right business opportunity or have advantages can do way more. So there is something there in that there is. So there's this um land rush starting. I think a lot of the people coming out of knowledge work are just anti- AAI and those people are going to struggle. I'm sorry but if you're anti-AI at this point it's like being anti the sun. You're going to have to go live underground, right? But the people who are like pro AAI like I I think we're going to see a big redistribution of who's doing the work and and where you get your software from.

**20:37** · And it may we may well wind up from I I I could actually see a happy place where Amazon's not even a thing anymore.

**20:45** · I I really could because software becomes we don't have the words for what's happening right where you know so many things happening this year that we don't have words for. Have you noticed that? But software becomes sort of like uh distributed. I don't know.

**20:57** · I do see non-technical people getting into software. Could there be a job there for engineers to come and actually take over maintenance? Yeah. I mean, I I think there's going to be plenty of opportunity for there's gonna be there gonna be a lot of engineers uh doing software engineering. I just think we're all going to be doing it with AI, right?

**21:15** · Yeah.

**21:15** · But I think it'll be quite some time before companies are comfortable trusting their code to be deploy written and deployed by AI without any human being involved at all. I think the the point that people are missing, the important point that the naysayers and the skeptics are missing is not that it's a AI is not coming to replace your job. It's not a replacement function.

**21:34** · It's an augmentation function. It's here to make you better at your job, right?

**21:39** · And uh that's not a bad thing actually. Uh I don't I don't know why people would fight that, but uh speaking about the job as as developers, you've said something that can be triggering for a lot of people. You've said that I think this was on the AI engineer summit that if you're still using an IDE now, you're you're a bad engineer.

**21:56** · Yeah.

**21:56** · Well, you got to be a little provocative. Yeah. Um you know, I I I let me put it this way, okay? I'm not going to say you're a bad engineer cuz I know some very very good engineers better than I am who are still at like level one or two in my chart, right? But I feel profoundly sorry for them. I feel pity for them like I've never felt in my life for these grown people who are good engineers or used to be and they they're like, "Yeah, you know, I use cursor and I I ask it questions sometimes and I'm really impressed with the answers and then I review its code really carefully and then I check it in and I'm like, dude, you're going to get fired and you're one of the best engineers I know.

**22:29** · Tell me about your chart. Tell me about your levels that you came up with.

**22:33** · Yeah, so I was drawing this on the board in Australia for a big group of people trying to show them what happens cuz I saw them at all different phases. Some of them had their IDs open. Some of them had a big wide coding agent. Some of them the coding agent was really narrow, right? You know, and so I was like, okay, we're going to put you all on a spectrum just to show what's going on, right? And level one, no AI, right? You know, and and and level two it's it's the the yes or no. can I do this thing, you know, in your in your IDE, right?

**23:01** · And then level three, you're like, yolo, just do your thing, right? Your trust is going up, right?

**23:06** · Level four, you're like the code, you're starting to squeeze the code out, right?

**23:10** · Because you're like, you want to look at what the agent is doing and not so much at the diffs anymore, right?

**23:14** · So, you're not reviewing as much now.

**23:16** · You're not reviewing as much. You're you're you're you're letting more of it through and you're really focused on the conversation with the agent. Mhm.

**23:22** · And then at level five, you're like, "Okay, I I just want the agent and and I'll look at the code in my IDE later, but I'm not coding with my IDE." At level six, you're bored because you're like, "Okay, my agent's busy. I got I got to do something. I'm twiddling my thumbs." And so, you fire up another agent and now you're addicted because you'll very quickly get into an equilibrium where every agent is waiting. There's always an agent waiting for you because somebody's finished, right? As soon as you spin up enough of them mathematically, right? And so, you find yourself just multiplexing between them going like this and you can't leave. practical question.

**23:49** · Assuming I'm working on the same code base, do how do you spin up the multiple agents so they don't get in conflict? Is it your are you going to use like Yeah. So that takes you to level seven, which is um oh my god, I've made a mess, right? I accidentally texted the wrong agent and didn't realize it and they did a big project inside of this project because I asked them to and now I got to clean up this mess, etc. Right? All that stuff. And that was when I started going, okay, what if we were to like coordinate this? What if cla code could run cloud code? That's the question everybody wants to know. And everyone was trying all last year.

**24:19** · It's going clog code. Run yourself. It would run for a while and it would stop, right? Y and and so it was the whole stopping thing that So yeah, I pushed on that really really really hard and and wound up building some some stuff to help with it. But uh yeah, boy, it's changed a lot, man. It's it's changed so much.

**24:36** · Going back to the ID, you you had a really good live debate with Natan So from Zed and the title was the death of the ID and both of you argued your view.

**24:46** · What what is your view about the ID and and also what did you learn from from Nathan on on like his take of he was a bit more pro ID and you were a bit more like maybe this is not going to be around forever.

**24:57** · Yeah, I mean you know I am where I am in my journey which is I I think that AI will do it all for us eventually and so the way I see is what do they really do and what are they really for. Okay, it's not really for writing code. It's for bringing tools together and for making a big tool, right?

**25:16** · Y and now you have MCP for that or whatever, right?

**25:21** · Uh and so I see IDE returning and I think cloud co-work is a return to the IDE form. It's it's cloud code going, oh, I need to be for real people, right?

**25:32** · But I think claude co-work form factor probably works better for the average developer than cloud code does, right?

**25:38** · So I see IDE I see us coming back into a world where it's ideides except it's all conversations and you know monitoring and this is a really good point. My brother built a thing called craft agents which is pretty similar to to cloud co-work except they connected in in their company their own data sources and he said that some developers start to prefer that because it's a visual that's easier to see. Parallel agents for example if you're not a power user it's easier to scroll it's just a nicer UI.

**26:04** · So your point on maybe some developers should try out like if if you're not sold on cloud code like try cloud co-work or any other similar more visual thing it might be more your thing but like you know get some people love the command line I actually just use the UI because I just don't like memorizing the commands as embarrassing it is to admit or maybe these days it's not as embarrassing.

**26:25** · Yeah

**26:25** · the key was try as long as you're trying something. Yeah. One, probably the single most important proxy metric that you can have in a company today is token burn because what token burn says is your engineers are trying to do stuff or your non-engineers. And when they're trying, they're failing and they're learning. And so if you want to get those organizational bottlenecks discovered early on and you want to get your engineers leveled up on my eight level spectrum early on and you want to solve your business processes ahead, you need to start now, which means try. It doesn't matter what you try.

**26:57** · It doesn't matter which tool you use. As long as you're using AI and you're trying to get it to do the work, you're doing the right thing.

**27:05** · Yeah. And I I think as professionals, like we really ought to just at least try. Like you get firsthand experience and then you can make your decision.

**27:12** · Steve's point about token burn is really interesting. The companies that win are the ones that experiment the most. And if you want to bring that same experimental mindset to your product, not just your AI usage, that's exactly what our presenting sponsor, Static is built for. Static gives you the complete toolkit without building it yourself.

**27:29** · You get feature flags, experimentation, and product analytics all in one platform and tied to the same underlying user assignments and data. In practice, it looks like this. You roll out a change to 1% of users at first. You see how it moves the topline metrics you care about, conversion, retention, whatever is relevant for that release.

**27:47** · If something was wrong, instant roll back. If it's working, you can confidently scale it up. Companies like notion went from singledigit experiments per quarter to over 300 experiments with static. They shipped over 600 features behind feature flags moving fast while protecting against metric regression.

**28:03** · Microsoft Atlassian and Brex use static for the same reason. It's the infrastructure that enables both speed and reliability at scale. Static has a general free tier to get started and propricing for teams starts at $150 per month. To learn more and get a 30-day enterprise trial, go to static.com/pragmatic. With that, let's get back to Steve's take on the state of Gast Town.

**28:24** · Now, there's a huge problem with people not knowing how to try and they say, "Oh, let me do something." And then it does the wrong thing because they always do. And then they're like, "Whoa, this is garbage." Uh, so, you know, you have to teach them that it's a shovel and you don't go shovel dig like in Fantasia, right? Like make the brooms walk around.

**28:40** · No, you pick up the shovel and you dig with it, but it's a shovel that you didn't have before you were using your hands. Like, it's a really really simple analogy, but people just don't get it.

**28:47** · They don't get it. And I think and I'm going to say something that's contentious, but in it's it's just the reality of the world. Most people can't read. I've ruined much much of my work in my life, I've just completely gone down wrong paths by overestimating people's ability to read. And I think that reading is, if anything, getting harder to come by as a skill these days.

**29:06** · And uh and this is the situation that we're in right now is that cloud code makes you read a lot. So I think we're in a weird limbo for the rest of this year, okay? where until the UIs arrive that are good enough for everybody who can't read, everybody who can't read is going to be a severe disadvantage.

**29:24** · Tell me a little bit more about your observation. A lot of people, a lot of developers cannot read because you were at Amazon that place supposedly is running on six pages and people actually reading does it I mean most dude most people can't read you. I don't know if you know this man like I they read really slow. Okay. And and the AI is I mean come on to most people five paragraphs as an essay.

**29:49** · Remember five paragraph scenes in high school is a thing we have in America. I guess maybe yours were 100 paragraphs in Amsterdam.

**29:55** · But to us five paragraphs is a lot.

**29:57** · Then that's like that's the AI just clearing its throat, right?

**30:01** · Yeah.

**30:01** · \[laughter\] You know, you got to be able to read waterfalls of text. And so we're looking at a world where that won't work. And so you're going to need recursive summarization. You're going to need a factory. And it's funny because like this is why I mean trying UIs is so important because Gas Town right now the reason I say you can't use it is that it's a factory filled with workers and you're talking to it through a telephone. You can also go and look through the window and pound on it and talk to the workers but it's not like you're in it right with a UI you're in it and you can you can see what's going on and right it's all invisible in yes by and large right you know hard to see.

**30:35** · And so I really do think and I and I'm going to I'm just going to make a bold prediction. And I think that by the end of this year, and we'll see demos of it like right away, but by the end of this year, most people will be programming by talking to a face.

**30:48** · A face as in a screen.

**30:51** · Your AI, like the Gas Town mayor, will be a fox talking to you. And you'll say, "Why doesn't it work?" And it'll say, "I'll go look at it." And it'll go spin off its workers just like it's doing, but you're talking to a face. And it will talk only. Yeah. I think that's the only thing that's going to work for most people.

**31:07** · Fascinating. Let's let's write this down to prediction. Why do you go build it? I'm not going to.

**31:12** · Let's talk about Gas Town. You mentioned Gas Town. What for those that a lot of people have heard about it, what is Gas Town?

### Gas Town

**31:18** · Gas Town is an orchestrator. So 2023 was completions code completions.

**31:25** · Yeah. Autocomplete. Yeah, that's when we said it's completion acceptance rate card. Do you remember that?

**31:30** · Oh my god. People were measuring it.

**31:32** · Yeah.

**31:32** · Stupid metric by the way. Uh the second one was but it was close. It was a proxy for are they trying right? Then there was chat that was 2024 right and then agents was 2025. We knew you could just look at that curve and go okay well if if chat is completions in a loop basically and agents are basically chat in a loop well then we're going to put or we're going to put agents in a loop and that'll be an orchestrator right and a bunch of them started coming out and I built one of my own my own vision but that's all it is it's agents running agents and can you talk through an a software

**32:03** · engineer through it architecture like how is it organized how can I imagine you know the setup yeah sure I mean look um Gastown is really complicated and it's been really broken all week because I'm migrating it to Dol and that's where I actually learned how complicated it was. It has a lot of features.

**32:18** · You're migrating it to to Dalt. It's a uh a new database.

**32:23** · Oh, okay.

**32:23** · Yeah, Dol is uh Dol is amazing. Dolt is a git back database. It's a git database. It's beads is just git plus database crammed together badly. And there's actually a database that does this. So, I'm I'm migrating to it. But yeah, anyway, Gas Town is is is what it should be is one one mayor that you talk to, that's your your person, and then whatever else needs to get done, they're just going to fire off workers. Okay?

**32:50** · It's a little a little bit more complicated than that because there are really I think there are two kinds of work that that that people go back and forth on and people are arguing about whether they're the right one. Some people at Anthropic told me it's the minimaxing context argument. Okay, there are people who believe that you should maximize your context window and fill it with rich juicy context so that the AI is wise and all knowing when it's talking to you. They want to like you know just right at the edge of the context. And then there are others who are like task kill it task kill it.

**33:14** · I want the shortest possible window because of the quadratic ex you know increase in in um cost combined with the dramatic drop off in cognition as the tokens go up right losing their track and stuff.

**33:29** · So so what which one's right? And we've got people who are like full on in the in the in the minimizing and and the the maxers. And and I looked at my work workflow and I was like, well, pcats are the min and crew are the max. I have two fundamental role worker roles and gas task.

**33:45** · So you have you have the the really simple one which is the small concept.

**33:48** · If you have a really if you have a really well specified task all broken down into subtasks, then you can find and and and it's like it's self-contained. It's it says what to do. Then you can give it to a worker and have it go do it, right? Meanwhile, you have a really difficult design problem.

**34:02** · You're gonna have to have a series of conversations about this. I maximize context. I'm like, read all these docs and then we'll talk. Right? So, it's just two workflows.

**34:12** · And like I I like the idea. I mean, it sounds like it's I think it's so easy to imagine like it's a little town, you know, like this wild wild west. There's the mayor, like the the crew, the the workers, everyone's buzzing and going around and the house are being built. In practice, how does this work? like how has it worked for you? How what what are you hearing people get projects done versus not getting it done versus turning into absolute chaos? What have you learned with Gas Town?

**34:37** · It's been a great experiment. I mean, I've I've really experiment, right?

**34:41** · Well, yeah. I mean, right. I mean, I went out and built something that doesn't that deliberately doesn't work. It's too hard. It's too hard for the models. Even Opus 4.5 is barely enough.

**34:49** · And it's funny because the folks at Anthropic told me they they like it, but they're kind of embarrassed some of them because it feels like I've got all these workarounds for bugs in their model, which it kind of is, right? But it's not a bug. It's their model was never trained to be a factory worker and it will be soon. So a lot of gas time is going to disappear. A lot of the complexity, a lot of the roles that are monitoring, all they're trying to do is tell Opus 45 to be smarter and that's being on the wrong side of the bidder lesson, right?

**35:12** · So a lot Gastown is going to simplify and flatten into just minimax roles.

**35:18** · crew for your max and your pole cats for your mins and and I think that's the natural shape and they'll just scale up and and could that be the pcast? They might just be sub agents at some point for example like well sub agent I mean you pcats are sub aents um it's just that they're they're more they're first class they have their own identity inbox you can talk to them you you can actually see how they performed over time by computing skill vectors on their their work and things like that. So a little little bit more than that than sub agents. I think sub agents have the problem of being opaque.

**35:46** · I'm going to fire off a bunch of sub aents to go do this work and then you're like okay let me know when you're done. Whereas with Gastown you can go look at them and be like dude your pcat's not working. I'm going to poke it. Right.

**35:55** · So, Gas Town gives you a lot of hands-on, I don't know, steering, right?

**36:00** · It doesn't try to be it doesn't try to get out of your way. It's in your way.

**36:03** · Gas Town, it's really fun, though. I miss it. It's been down for a few days for me. And I tell you, man, working with regular Claude just stinks by comparison because it's like an idea factory. Once it's actually running and all booted up and everything, you can have so many things going on at once and actually track them reasonably well.

**36:20** · Now, it can suck you into a a mode where you don't sleep, you don't eat, and you start it's not good for you. And I actually wanted to talk to you a little bit about what's what's happening in the industry at some point. But but Gas Town itself, I mean, like it was all calculated, all the characters, you know, the naming. Why did I even do Gas Town, right? Why is it why?

**36:40** · Because I wanted to move the Overton window, right? Because people last year when I would say orchestration's coming, they'd say no agents aren't aren't no swarms, no orchestration, whatever.

**36:51** · Everything you're saying is just not true. And now what they're saying is, bro, you're being pretty aggressive, right? Which is a different conversation. They're like now they're like, well, your swarm, I don't know, maybe your swarm can't do blah blah. But it's just completely shifted the conversation from the realm of impossibility to the realm of possibility. So, is is it fair to say that you took on more than you you reasonably thought you could chew? You took on this more ambitious ones because you wanted to both stress test what these models can do.

**37:21** · Uhhuh.

**37:23** · And find out find out and honestly just have some fun.

**37:26** · Have some fun. Find out what's next. And I'm continuing to do that. So, my next thing is I'm going to string 100 gas towns together. We have a community, a Discord. And if Molt book can get people to pitch in tokens for fun, like they paying they're paying you're paying for the inference of your your agent on Moltbook, right? So if I string a 100 gas towns together and we decide to build something together, we will learn the mechanics of Federation, we're probably retracing Ethereum steps, but we will. And uh and we're going to come up with something remarkable.

**37:54** · It's like the people version of MoltHub uh right malt book, whatever it is. And what what are misconceptions about Gas Town or what it's trying to do that you feel it's kind of, you know, gone off a little bit of rails and is good to clean up?

**38:10** · Well, I mean, for starters, I don't think people should be using it and they are. And I I really mean it.

**38:16** · When you say people should not be using it, like not should not be using it except if you're doing research or or if you're like actually understand that this is just a proof of concept. So, some some very very clever people that I've been talking to have have been searching their problem spaces for subsets, categories that Gas Town could productively use today at a big company, a big Fortune 50 company, say.

**38:38** · Wow.

**38:39** · And they've they've identified some problem spaces that you could put Gast Town on today. And I was like, oh, that's pretty pretty clever thinking.

**38:45** · One of them was this company I talked to that sets up bespoke data centers for you, okay, in any region you want, which is something AWS has never been able to do. Google's always tried. and they say it's just three months of miserable button presses to try to install the software and check that it all works.

**38:58** · And the acceptance criteria are very clear. It's, you know, it's almost a Ralph loop, but they think Gas Town could swarm it and and eventually converge on a data center that works and and save all the people the trouble. You know what I mean? And I was like, all right, all right. And this could potentially meaningful move the needle on their ability to open up more of these data data centers for people, right?

**39:17** · Wow.

**39:17** · Yeah, go figure. Uh, and the same guy was telling me that he's been looking at production incidents and he and he's realized their system is already in an indeterminate unknown broken state when they're down. So, how much worse can AI actually make it? Now, I cautioned him and said actually it can make it a lot worse. But he's thinking along the lines that there are certain categories of outages where you could have them in investigation mode or whatever, right?

**39:36** · Where they could speed things up. So, people are looking for the fuzzy problems. There was a third one that came along. I forget what it was, but there's there's a classes of problems emerging for which you can swarm them because you don't care that the results are messy. It's the cumulative work that Right. But that's actually how I code now. I mean like Right. I mean like I code myself. I mean I bit off more than I could chew. There's no question about it, man. Gas Town is a huge mess right now. And everybody's going he's going to vibe coat himself into a corner and come crying out. You know, they're pretty close to true. Although I did manage at just before we got on the plane to get it back on track and it's working again.

**40:07** · Right.

**40:07** · So one interesting about Gas Town is you said you don't look at the code, you have the agents write the code and which is very very unlike what your career has been, right? you cared about craft code, elegance. Why did you decide to do it?

### New ways of working

**40:21** · And what are the results? I mean, are the results as bad as I would think they would? Cuz this is right like like if if you imagine we're going to put like a thousand interns on a project like we've kind of seen that in the past and the result has been well eventually a senior engineer comes in and cleans up the mess. And I'm I'm just curious like how how is it better or worse? Well, so the ceiling of what it can actually build productively before it just dissolves into a mess is going up.

**40:47** · But right now, I think it's sitting somewhere between a half million and five million lines of code somewhere in there. Probably more on the half million side right now. And with the next drop of an anthropic model, we're probably going to see it jump up to a few million lines, which is pretty good size, but it's nothing compared to what enterprises have, right? Nothing.

**41:03** · Enterprises are very, very, very, very big. They have hundreds of millions to billions of lines.

**41:08** · Yeah.

**41:08** · But not in one cold base. like h having a few million lines of code is already a big code base and you'll typically have 50 plus people sometimes 100 plus 200 plus working on it right what what it really comes down to just to to summarize this conversation get to the end is how well you're going to be able to take advantage of AI totally depends on whether you're a monolith or not if you're a monolith

**41:26** · which almost every company is a monolith they have one monolith and a bunch of microservices right if you're a monolith you're kind of hosed because I told you the ceiling's going up for what they can do but it ain't never going to hit your monolith that will never fit in the context window and you're never going to be able to never in the next 18 months be able to tell a model, go fix my monolith, you have to break it up. Okay.

**41:44** · If you want to take advantage of AI or rewrite it from scratch, it's starting to get faster at this point to think about rewriting your stack. Yeah.

**41:50** · One thing you you mentioned even before we started that AI can really drain you.

**41:55** · It can drain your energy. It can pull you and it can suck you in. Can you tell me about this?

**41:58** · Dude, there is something happening that we need to start talking about as a community, as an industry. Okay. There's a vampiric effect happening with AI where it gets you excited and you work really really hard and you're capturing a ton of value. For me, I'm doing it all for myself and it's still kind of like pushing me to my ragged edge. I find myself napping during the day, but I'm talking to friends at startups and they're finding themselves napping during the day. It's funny. They they literally try to load each other up with enough context to force the other one into a nap.

**42:28** · Almost like a con a comp, you know, compassion event. It's so weird. And we're starting to get tired and we're starting to get cranky. And I started talking to people in the industry and they're starting to get tired and cranky. And what's happening is see companies are set up to extract value from you and then pay you for it.

**42:50** · Right? But the way all companies have always been set up is that they will give you more work until you break. If you can do it, they'll just happily just say, "Give you more. I give you more until until you your your plate flows over and you die." And people have to learn the art of pushing back, right?

**43:04** · And that's been a thing for a long time.

**43:06** · But it's changed the equation. The way you push back, the reasons to push back and all that have changed very dramatically and and are changing right now because you've got all these people now who can be super productive. And it's like, let's say an engineer can be 100 times as productive just just for sake of argument. All right. Who captures that value? If the if the engineer goes to work and works for eight hours a day and produces 100 times as much, the company captured all of that value. Y and that is not a fair capture exchange.

**43:33** · I think we can argue unless if they have early say sharp and they have a meaningful equity that's a bit different. It grows for but that's not the majority of people right? It's a minority.

**43:43** · Yeah.

**43:44** · Yeah.

**43:44** · We're probably getting there pretty quickly. I I didn't you know we did notice one thing like and you probably saw this as well about six months ago. We talked about a lot, the 996 problem at AI startups. And we we were like, "Oh, it's interesting. AI startups, people are working really freaking long hours and they're posting that they're in the office at 3:00 a.m.

**44:02** · And you could tell I'll share with people what 996 is who don't know." Okay. 996 is uh 9:00 a.m.

**44:09** · to 9:00 p.m. 6 days a week, if I'm not mistaken. Yeah. Which is which is 996 is it's the standard you're expected to work in most of Southeast Asia, as far as I know. Uh I I haven't been to China or India, but I assume it's pretty much similar there too, right? There's another group of people who are uh capturing all of the value for themselves. Okay? They go in and they work for 10 minutes a day and they get 100 times as much done and they don't tell anyone and they've captured all the value. And that's not really ideal either, right?

**44:38** · So, uh at least in terms if if you're thinking in terms of how can groups of people be successful, it's best if they're uh all contributing, right? So, what do you do? And I think that the answer is each and every one of us has to learn how to say no real fast and get real good at it. And we need to learn how to start capturing and the correct this is the new work life balance. Okay?

**45:00** · It's how much of the value are you going to capture from being 100 times as productive and how much of it are you going to pass along to your employer.

**45:05** · And this is a really difficult place to be because we don't have any cultural all our cultural expectations are pointed in the wrong way for us to work harder and they want us to right everyone wants to extract extract extract. And so I I seriously think founders and and and company leaders and engineering leaders at all levels all the way down to line managers you're going to have to be aware of this and realize that getting your engineers onto this this treadmill is pulling them into they're using much much more of their system 2. you know, they're doing much much more of that hard thinking.

**45:33** · Now, the easy stuff is getting automated by So, you're you're actually draining them at a higher rate. Their batteries are draining at a higher rate. You might only get three productive hours out of a person at max vibe coding speed, and yet they're still 100 times as productive as they would have been without AI. So, do you let them work for 3 hours a day? And the answer is, yeah, you better or your company's going to break. It's very interesting because also like the the value extraction I think I I can see us speeding up and we see it with a few prominent people.

**46:02** · Peter Shinberger single-handedly pushes out so much more value output you name it commits in any way that would have been a team of 10 pretty good engineers before and he you know like in all fairness he is capturing it in the sense that he's it's his project it's his baby. He does not sleep much.

**46:19** · Uh so so that that's definitely showing but the value capture there is kind of okay but I I agree with you that this could be something really like in the past whenever there was a technology shift where people were more more efficient we couldn't in in your lifetime have you seen this where injuries became more efficient and suddenly you could do a lot more with a lot less and what happened at that time people got mad example Pearl the Pearl programming language was a massive accelerator Amazon's website was built in Pearl probably still is actually I think Facebook's technically is PHP is a fake pearl.

**46:50** · Um, and you can quote me on that. So, and both of them were incredible productivity accelerators and everybody just could see it. You don't want to build websites and see, you just don't. Amazon tried it and they gave up, right? So, that caused a a huge rift, a huge schism. There were secondass citizens. All kinds of cultural dynamics happened there. Right.

**47:11** · I'm curious about how some AI companies deal with this. Can we talk about how Entropic works?

**47:18** · Yeah.

**47:18** · Yeah. from what I know from from from what what you know from the outside I I know that you know you you talk with like people across the industry but Antroic is a very interesting place one interesting thing they Dario recently said is he thinks compensation specifically uh for for

**47:35** · their staff the people who are building all these things and they're actually using the models and doing he said something interesting that maybe we should have compensation where people are compensated even after they leave the company for the value that they created which is just something completely unheard of, but it's clear that that he's thinking about this this thing that is changing where you can you as individuals can create massive value in a relatively short amount of time.

**47:58** · Google, you can send me a check for all that stuff you never paid me for. Okay, just got to get that out of the way. I like that idea. Anthropic is unlike any company on Earth right now. They're operating in a space that is really fragile and they're very protective of it and they need to be uh because uh they've they've created a hive mind. uh they're running the company as far as I can tell like a pure functional data structure. Remember Crystal Kasaki's book? That was such a mind-blowing. You can make data structures that never mutate. Then how do you mutate them?

**48:28** · Right? And the answer is you just keep adding. It's improv. Yes. And yes. And right and that's how they operate.

**48:34** · And when you say hi mind, what what do you mean by that?

**48:37** · It's it's a lot of it's like the markets today. Vibes. Everything's vibes. It just shifts. It's just right. It's it's it's vibing. It's it's kind of hard to explain, but you see here's the thing, right? We used to build products by like making a spec and then implementing it and then complaining about it and then shipping it, right?

**48:53** · Having a road map and planning for it and waterfall and timing it for the company annual event, right? Apple, right, once a year. The way you work with like systems like Gastown and they've got their own internal orchestrators is you create and your founders the one that like the co-founder that was nontechnical you create the prototype and that's your product and you start building it and you just make it the product until it's right. So everybody just gathers around the prototype like a campfire and builds it and that is what Anthropic is doing at scale with thousands of people.

**49:21** · So you're saying that the playbook of a successful tech product might have changed because the traditional wisdom since the lean startup in like 2010 or so was you use your prototype to get signal then you throw it away and then you build a lot more polish stuff right you and we used to I think every

**49:39** · software engineering who's been around you don't ship a prototype you tell people it's a throwaway you start again you make it production ready scalable that kind of stuff because you don't want to give a bad experience to people what changed though just the ability to do infinite number of prototypes So instead, you make prototypes until you get a great one and you're like, "Let's launch this." And so apparently Claude co-work happened in 10 days. Somebody went, "Hey, I did a prototype." And they were like, "We're gonna launch this." And 10 days later they launched it. So I mean, it works.

**50:06** · But I guess one one important context there when I talked with Boris Churnney about a feature that they did about how they did the tasks in CL in cloth code, the task list of how it completes. He told me that in two days he built 20 different prototypes that were all working thanks to AI. I didn't know that but he's doing what I'm talking about.

**50:23** · They call it slot machine programming like you do 20 implementations and is that what he's doing?

**50:28** · Something like that. I I don't want to put words in his mouth but but I was I was just floored because building 20 working prototypes that would have been two weeks and and and you would have not you would have stopped at three, right?

**50:39** · That's in our book actually if I can pitch the book for a moment. The fafo f a fo is the dimensions of value that you get from vi coding and the o is optionality which is the ability to create lots of prototypes. What it lets you do is defer your decision until you know what the right answer is which is cheating. So of course everybody does it right and it's going to fundamentally change the way that companies are run.

**51:02** · It's going to change the way that people and organized to create software and it's going to happen this year.

**51:07** · It's it's just fascinating how these changes are coming. But what what enables the these changes? Is is it the fact that we can iterate faster with these things? Like I I look I saw a phenomenon happen at Google. This is this is kind of a big company question. There's kind of two there's a big company and a small company answer to your question, right?

### The problem of too many people

**51:25** · So something happened at Google. I went through the golden age at Google where it was like anthropic. It was a hive mind. It was nobody was mean. Everybody was innovating and it was wonderful.

**51:36** · Yeah.

**51:36** · This was a time where like the founders were pretty close. you you go to the cafeteria and Larry and Sarah be sitting there and you'd hang out with them and just chat and it was like gold mage, right?

**51:46** · Yeah.

**51:46** · And then it changed rather abruptly. We made a few pivots and it became not that company anymore. And in fact, innovation died on the vine like altogether and since I don't know 2008 there has been no innovation from Google. It's all been acquisitions. They have they've created nothing new.

**52:03** · I mean I mean they they did Gemini a few years few years later, right?

**52:06** · Gem G. Yeah. Okay. Sure. They created LLM and then did nothing with them. That's a perfect example of why innovation dies there.

**52:12** · Yeah. For five years, right? Five years they did nothing. So I don't count Gemini. That's a different Google. Yeah. Okay. We're talking about the Google that screwed up.

**52:20** · I don't want Anthropic to screw up this way again. The the way that Google did. Google put safeguards in place to try to keep them from turning into the company that they turned into, which was oified, you know, territorial. Nobody could. I hired a brilliant dude from Microsoft, brought him into Google and said, "Figure out what you're going to do.

**52:38** · Take as long as you need." It took him six months to find something that nobody else had claimed already. People claim work and then never do it at Google. So, I'm going to tell you something I've never said before. This is brand new take. I think what happened at Google was when Larry Page became CEO and he said, "We're going to put more wood behind fewer arrows." That was a motto.

**52:58** · And he put a halt to innovation. Okay. Before then there was more work than people and after that there were more people than work and so people started to fight over the work and that's where people started to do land grabs and backstabbing and territoriality and empire building and all all the bad

**53:17** · stuff you see all the politics that you see is about fighting over work and going back to anthropic they're at a frontier and there's infinite work and like literally all of them have too much to do and a friend of mine a friend of mine at Amazon once told me But we don't have a lot of the problems that Google has because everyone at Amazon is always slightly oversubscribed. They have too much work.

**53:37** · I I've heard similar with Apple as well that that that's kind of deliberate.

**53:41** · Interesting thing. I mean, if you assume I am seeing productivity gains for myself, so I'm not disputing that agents actually make you more productive and I think we can agree on by how much, but for me it's a lot. But if this happens a lot of companies, people can actually do a lot more work. Do you think a lot of companies that are larger will see politics show up which typically hence happens when if if you're right if like the catalyst for the bad stuff beginning is more people than work and all of a sudden people can do all the work.

**54:11** · Yep.

**54:11** · Then the company's biggest problem is going to be finding more work or they're going to have to get rid of people which is kind of bad, right? But it's it's not unlike Gas Town in the small. My biggest problem with Gas Town is feeding it because it works so fast. I have to I have to work really hard to come up with good designs for it, right? That's what I spend all my which this is why I'm taking naps all day on because I'm trying to come up with difficult work for it. Right? Other people have said this too. This is this is the problem with gas and this is the problem with everybody who's going to use any orchestrator. It doesn't have to be Gas Town. That thing will be dead in 4 months probably. Right? I mean it's it's the shape that worked in December 2025.

**54:41** · That's not going to be the shape that works in four months, right?

**54:43** · One thing that I think you know we're it might sound that we're talking really abstract especially for people who have not done this type of work in the self is like well we're talking about orchestrators they're like all productive. Can you point to something that has been built with an orchestrator or with this higher productivity that is a production software either you built it or you've observed someone build it that could show like actually this is way more productive and we can actually see the output or turning it the other way around like we're still not seeing that much more output from companies teams that you would expect.

### Why AI results lag in business

**55:12** · Okay, like a lot of them are are having more productivity, but like from the outside, it's easy be to be skeptical when we're seeing not much has changed in terms of our day-to-day life the apps, you know, we're seeing signals here and there, but nothing major. Like why might that be?

**55:29** · Yeah, that's fair. Um my my feeling is that probably uh people have a low tolerance for non-determinism and um these things are fundamentally nondeterministic. So they can't just go replace customer call center software because they they could be wrong. And it doesn't seem to matter that humans are also wrong very often. And AIs can these days can very easily get to the same level as a human as an average human in the job. But I think there's still still a lot of risk aversion.

**56:01** · Right?

**56:02** · So I think that the companies that are actually running with this are actually starting to see the results and it's going to be reflected in their quarterly earnings invisibly and in other ways at first. Could it be that we're we're focusing on on building the tools?

**56:13** · I'll turn it around and I'll say what if what we're actually observing is that innovation at large companies is now dead and we are only going to see innovation from small places which is kind of what happened when cloud came out and Facebook was a college kid at one point. Facebook feels like the biggest company in the world right now but it was one dude. Okay. And so when a new enabling platform technology substrate appears, you're going to see innovation at the fringes because of the innovator's dilemma. Big companies can't innovate. They're all running into this problem.

**56:44** · They may have hyperproductive engineers who are producing at a very very high rate, but the company itself can't absorb that work downstream. They're just hitting bottlenecks and these engineers are getting shut down and they're quitting. Right? So I think what's happening is we're all looking at the big companies going, "When are you going to give us something?" And the answer is we're looking at the big dead companies. We just don't know they're dead yet.

**57:03** · Do you think they're dead? Because for example, it's it can now be cheaper to do something like we couldn't just say the eternal punching bag zenas customer support. They have been the de facto place to do your customer support because your agent can sign up. They get this UI, they get this workflow, etc.

**57:18** · And for AI native companies that are using MCPs, whatnot, it makes no sense for them because they just want an API which Zundas does not want you to give to you because they want to charge extraordinary amounts for you to come to their platform and buy their AI for, you know, 10 times the cost.

**57:32** · That model is going to struggle a lot in coming years because people will build their own stuff bespoke with APIs. This is this is this is my platform rant in real life, right? If Zendesk doesn't make themselves a platform, then they're going to they'll have producted themselves out of existence, I think.

**57:46** · And the platform for the for looking ahead, it's is it API? Is it is it MCPS?

**57:52** · I mean, as far as we can no maybe not MCP, right? I mean, what what did Anthropic found that what works better than MCP is having the AI write its own API to call the MCP because they're so good at writing code, but then nothing really changes because platforms are always APIs from the beginning, right?

**58:08** · Yeah.

**58:08** · So, why do we need MCP? Well, we needed some way to declare what the tool does in an AI way, but I mean like I just it's so loose and so flexible. Integration is going to be really easy.

**58:16** · I don't know. I'm not following that space well enough to know if MCP is going to continue to be an important dominant player or if the AIs just use stuff directly like via command line tools, right, or APIs. But either way, um we're moving into this world where um uh the innovation is coming out of uh new shops who have who have adopted and adapted and and I see big companies struggling really bad right now with this. I wonder if these if if if we we will see a lot more of these building blocks that we didn't know we needed.

**58:48** · Dude, I I I think we're going to see a huge ecosystem of building blocks for people who are non-technical who want to build stuff and they need those APIs and they right you know what I mean like for storage or for matching or for whatever it is they need to do. So, so, so I guess if you're in tech and if you're looking for an idea either because you know like your job is looking a bit shaky or you actually just want to do something like now could be a great time to start building some of these building blocks that we're going to need like reliable building blocks will probably be in need that are are that have state

**59:18** · that have SLAs's whatever have some some some importance right that's not trivial to do that's right because AIs are lazy uh and with good reason they don't want to burn tokens if they don't have to so if you provide a service that's going to make something convenient for them they'll absolutely absolutely use it.

**59:34** · Yeah, especially if it's a service that you you need to maintain, for example, like you need to keep up with may that be regulation or changes or logging or whatever. Yeah, that's kind of a lot of work to do even to prompt like to and go back every day to prompt again to like update and all that. Also, as humans, we're also lazy.

**59:51** · Yeah. I mean, well, Larry Wall called it, right? It's that's one of the virtues of a programmer.

**59:54** · Yeah. I want to go back to one of another one of your essays from 2012, uh, which was called the Borderlands Gun Collector Club.

### Gamification and product stickiness

**1:00:05** · You're the one that read that one.

**1:00:06** · I I got recommended on Blue Sky and and a lot of people liked it and I read it and I realized I didn't read it. And this was a really interesting essay because seemingly it has nothing to do with what we're talking about, but you talked about gamification and you talked about how this Borderlands game, which you played apparently, right?

**1:00:22** · back in the day. You mentioned how after you completed the game, there was this weird thing that the game developers probably accidentally put in there. People kept coming back to have like custom guns. And these were like a metag goal that the designers probably never thought of, but it actually made the game pretty kind of addictive. And you you called this as a I think it was like some sort of elder game or or something like that. And you were kind of saying that, hey, this was pretty smart. there was accident from the game designers, but maybe more game designers should do this because it just makes the game addictive.

**1:00:51** · And you know, like not saying that, but since that was in 2012, I've we've seen so many games just have like deliberate gamification and not just games, but but a lot of other things.

**1:01:03** · Yeah, a lot of them found that mechanic eventually. What who is it? Did the Borderlands um take two or I forget.

**1:01:09** · Anyway, they figured it out early, then they didn't capitalize on it. But uh yeah, so interestingly I think yeah gamification uh gamification's kind of rearing its head. People have pointed out that like people are making game front ends to gas town, right? I mean why not make it a game? Like come on, man. I mean like look, we have literally we have games for running factories.

**1:01:28** · Imagine you're running an actual factory. How cool is that, right? That's what guess what gastown is. That's why it's so fun actually. And do you think that one of the reason that some of the agents are more successful than others looking at specifically cloud code is they also did some gamification where there's always something showing there right there's a tinkering there's the there's the different things that keeps talking to you there's always

**1:01:52** · is is some of maybe accidentally or maybe deliberately oh I they they have the best product managers in the world and they have uh they have done absolute magic with command line UIs and stuff that they've done it's it's But look, I mean, come on, right? That's not going to work for most devs. So that's why cloud co-work is so cool, right? Because it's it's the direction that things are going to evolve. I think Yeah. So I think developers will use cloud co-work or something more like it with with traditional software.

**1:02:21** · We have tech depth and we we know how to deal with it and we've talked so much of this. In fact, if if we think about like what what we spent we're very busy with the 2010s tech collecting it paying it off migrations yada yada yada. Now that we're doing you know a lot lot of vibe coding or you call it v coding but agentic engineering just turning out a lot of code how do you think we will recognize or deal with or do we need to deal with this like v coding depth or agent depth?

**1:02:47** · You do you do one of my upcoming blog posts is about this actually I've discovered that there's a thing I've given it the name of it's called a heresy okay that happens in vibecoded code bases that you're not looking at where an idea can take root among the

**1:03:03** · agents that's incorrect it's it's there wrong architecture or or wrong data flow or whatever that's that's causing an impedance mismatch for the rest of your code and what happens is I call it a heresy because they have the tend they have a tendency to uh to grow and to come back and they're really hard to weed out. Okay. Uh I had a bunch of them in Gast Town. There was a polecat heresy that kept coming back.

**1:03:24** · And so what would happen was it's invisible and your your your product stops working properly along the edges and you don't know why and you start having the agents dig into it and you realize you've got a fracture. You got a fault line. you have like say two complete databases that are both live and operational and you're randomly choosing between the two of them, right? And you didn't realize this until just now, right?

**1:03:50** · You you find terrible, you know, things in your code, right? Uh and you try to get them all out, but there will be one reference to it in some doc somewhere that an agent picks up on and goes, "Oh, that makes sense. It's the heresy." And it returns and the agent does the wrong thing and goes off and rebuilds the heresy and it starts to spread again. It comes back, right?

**1:04:06** · It's like the agents want the system to work this certain way and you're telling them, "No, I want it to work this other way and and you're fighting with them and you what you have to do is you have to actually document the heresy in the beginning of your prompting and say, "This is one of the one of the ways that you can go wrong on my project. Don't do that." Right? And then you have to remind it periodically or even put in tooling to keep it from doing that. Another heresy is that my agents all think they should be doing PRs. It's like I'm the maintainer of this code, man. Just push domain, right?

**1:04:35** · Or a branch or something. and don't make a PR. It's just polluting the PR space. That's for contributors. They can't get this today. Now, I could put a bunch of hacks in, but that's fighting the bitter lesson. Opus 5 will be fine. Opus 5 will be, "Oh, you don't want PRs? I won't do any PRs."

**1:04:50** · What is the bitter lesson? And oh, the bitter lesson. Yes. Richard Sutton wrote a very, very short essay.

### The ‘Bitter Lesson’ explained

**1:04:55** · It's like 800 words. It's one of the best essays ever. What called the bitter lesson where he's like, "Yeah, we uh we're AI researchers and we learned a bitter lesson and you need to learn this lesson." The bitter lesson is don't try to be smarter than the AI. Okay, you think that you've got special knowledge that humans bring special domain knowledge to this problem and we're going to teach it so that the AI will be smarter. What we found was bigger is smarter always more data, right?

**1:05:20** · Yeah.

**1:05:20** · And so like when they're going into Australia right now, you know, you've seen the drawings, you know, how big OpenAI's training center was, how big Anthropics training center was, and now the training centers that are being are, you know, 10 times larger. They're massive. They're in Australia because they have all the energy and the land and everything, but they are going to make models that are 10 times or more smarter than the ones we have today.

**1:05:40** · Right.

**1:05:40** · We talked about the the vibe that, but does it not pain you? I mean, as someone who has built software, you know how to build good software. You you went in there to clean up the mess of junior teams or like messes you you were you could clean it up and with your eyes closed or maybe had to keep it open.

**1:05:54** · Does it not describe the AI going off and doing it if you scaled it back and said like hang on like let me step in let me make these decisions let me be the architect it would not happen.

**1:06:05** · Yeah. Well see the thing is I've also been a vice president at big companies of engineering.

**1:06:11** · True.

**1:06:12** · And so when I'm working with a team of 80 agents it's not very different from working with a team of 80 engineers. Any one of them can screw up too engineers.

**1:06:20** · Oh and you've done that right? I have and I'm telling you they are isomorphic. So what is the bitter lesson? The bitter lesson is don't try to be smart, just try to be large. Okay. Now that's not the only way to make the AI smarter.

**1:06:34** · They can also make them smarter in and a couple of other important frontiers that are also getting developed. And so to tie it full circle to a beginning of our conversation, everyone who believes right now that that the curve is S-shaped, they're 100% correct. They are 100% correct. It is S-shaped.

**1:06:51** · Eventually, we will run out of resources. The world will be out of resources and it will flood, right?

**1:06:57** · But I can tell you that there are at least two more cycles left in this. And that means they will be at least 16 times smarter than they are today. And that is going to cause all of knowledge work to be subsumed by this stuff. Before we go all the way there, let's talk about how all this the better models more productive could impact personal software things that that that people can can build themselves.

### The future of software development

**1:07:21** · This is what I thought you were asking about earlier when you said you wanted an API from Zenesk. Think about it. Everyone's going to want to build their own software.

**1:07:28** · Oh, I I was talking about a business for for not not personal but Oh, business is name. But but but yeah, but but also personal software like what what would the future look like when everyone could have like Open Claw running in in their closet or Gas Town or or they can just they don't have to run it on their thing but they can turn to this agent.

**1:07:44** · Yeah.

**1:07:44** · How could that change like both personal software but also the software industry as a whole? Cuz for a long time personal software was the privilege of us engineers who could build it and we built our tools and we had open source and we had some billion dollar companies grow out of some of the cool things.

**1:07:59** · What what do you think could happen now that this this will be democratized to some extent? How do you think open source could change?

**1:08:06** · Open source, how would open source change?

**1:08:09** · Could it could it have changed? Cuz one interesting thing that I I'm seeing is a lot of remixing happening. So people, you know, now a lot of open source projects don't really take poll requests because there's a lot of not great ones. But a lot of people are just remixing.

**1:08:21** · They're just taking the open source project. They're telling the AI make this change and they publish it as open source as well. Often no one looks at it. But now people are like weaving things together. They say take this project, take this thing and it's actually a lot more open.

**1:08:35** · I see what you're saying. In the old days, the f-word fork you used to be like kind of a declaration of war.

**1:08:41** · Yeah.

**1:08:41** · Like if you forked somebody's project, it meant you had had enough of them. Like Rode forked Klein and then somebody else forked Ru Code and it's just like I think it's now going to be an everyday occurrence, right? Good because it used to be that to fork it it would be a lot of time and effort to maintain a fork to merge back the the thing cursor is a fork, isn't it?

**1:09:02** · It is.

**1:09:02** · Yeah, that's a lot of work. That's a lot of work. Yeah.

**1:09:04** · Um a lot less work now, right? So, uh yeah, everyone's going to be forking. So, yeah. No, I think that that's a that's a natural Yeah. consequence of of of um everybody writing code.

**1:09:15** · Yeah.

**1:09:16** · Just like everyone can take a picture now. That didn't used to be true.

**1:09:19** · Yeah.

**1:09:19** · What what are some of your beliefs from early on in your career that held really really well until recently and now we've just abandoned because of AI?

**1:09:28** · \[laughter\] Engineers are special. There's one.

**1:09:32** · Come on. We are special. No, I think we're so special. We can Yeah, sure. We learned how to do something by hand that computers can do now. Kind of cool, I guess.

**1:09:41** · What about the engineering mindset? We we have that like it's not just coding that we do, right? Well, look, for one thing is I believe that our thirst for new software will never ever ever diminish. It will only grow. And so we're at the beginning of software. All the software we have right now is garbage. That right there, OBS especially. And we're going to see a new world over the next 10 years where software is commonplace and good. And you'll have your choice.

**1:10:06** · And it won't be I have to pick and choose between three really bad OOTH solutions or or company HR systems or whatever stupid ass thing, right? Like today the selection is terrible. SAS is awful. The whole the whole right airline apps.

**1:10:23** · Airline apps, right? Uh I mean we we we ran a vibe coding workshop in Sydney where a dude actually wrote an airline checkin app for himself and got it into the Android queue before Southwest realized you and shut him down because he was a bot. But that's what people want. They want personal bespoke software and they're gonna get it.

**1:10:39** · And so, yeah, I think you're gonna see that's why when Jeffrey Emanuel forked beads, I was like, you go, you go. He's I feel so bad about it. And I'm like, dude, this is the new world, man. Fork, fork, fork. Let's have beads in every language. I don't care. Right. I mean, in all fairness, like just looking at it from the positive side, like I wouldn't mind just having good software for the stuff that I use dayto-day. My utility provider is some of it is getting better. the the government websites that I have to access my my paying my parking fine. The other day I tried to send a package to Canada from the Netherlands and the post like the official post has been broken.

**1:11:10** · They cannot send anything for a week and I see the exception they cannot fix it. So I have to go DHL and pay a bunch more money.

**1:11:17** · That's right.

**1:11:18** · And like there's a lot of bad software out there.

**1:11:21** · Yes.

**1:11:21** · And your agent will be dealing with it, not you.

**1:11:24** · Yeah.

**1:11:24** · But I think people who write software that agents like and prefer and choose and then they find a way to market it and get the agents aware of it, they're going to win big because uh everyone will use agents. We'll all be dependent on it.

**1:11:37** · Well, plus also I guess software or ways of making agents write quality software because I I have a feeling like you you will want to do better stuff that if if you do the same, you're not going to have a business, right?

**1:11:47** · Yeah.

**1:11:47** · So, I mean look, I think businesses will compete on more and more complex software. The ceiling will just keep going. We're building like we're gonna until we build the Death Star or whatever, right? I mean, like we're we're building bigger and bigger things. Oddly enough, Gay, I am an optimist through all of this. That's my first belief. I think first and foremost is that it's all going to work out.

**1:12:05** · So, asking the optimist now, I got this question of I think it was on blue sky.

**1:12:10** · This person asked like how do you think the software industry will continue to exist if we get to the point that any software could be trivially cloned?

**1:12:18** · Yeah.

**1:12:19** · Where will that leave us? What what cannot be cloned? What what is the moat?

**1:12:23** · Ju just we we we just jump ahead. We assume that this these things actually can do connections human connections are probably the biggest one as as you know kind of almost counterintuitively as software does more and more automated for you people are going to be like oh well yeah but that's that's just automated I want a human to do it and they will literally want a human to bring their thing instead of a drone you know they'll they'll they'll want humans to curate things for them and I I think that's going to be humans will be a moat.

**1:12:49** · Do you think if you look back at some of history like like from you know the history of the rest history like have we seen some changes that felt a bit like this and then we saw some professions thrive because of either more automation or you know like stack overflow I don't know uh I mean like

**1:13:05** · that one jumped to mind uh mechanical turk like we've seen a bunch of weird big step functions it's just that we're we're about to see a whole bunch of them at once right I mean look at the news lately I mean like you you like this is the funny thing is everyone's like where's all the innovation and then in the news all day long they're seeing all this innovation in AI. It's just not coming from, you know, the Walmarts and Microsofts. It's coming from random individuals, right?

**1:13:28** · But the innovation's there and uh from the startups that I've been talking to, you know, I've been talking to anywhere from two, five to 20 person startups.

**1:13:37** · I think we're going to see some really impressive stuff launching in the next couple of months. Are are you seeing these small startups change how they work?

**1:13:44** · Oh god, it's so different, dude. It's so It's so different. Okay, for starters, for starters, I \[snorts\] think in the new world, I'm I'm convinced of this. Okay, everything that you do will either have to be fully transparent or you're hiding it for a reason.

**1:13:59** · Tell me more.

**1:13:59** · In other words, if you don't want people to see what you're doing, just don't show it to them and they will never see it. And if you do want if you do want them to see what you're doing, then you had better get it out in front of them as you do it instantly or else the train will pass you by. So like what they're saying is like so I told the story on my blog, people have heard it, but they like yelled at a teammate. They were mad because he implemented a feature that they'd asked for two hours before and they were like two hours ago it's changed too much since then, right? And he's like what do I do?

**1:14:24** · You know what's happening is they're they're getting into this mode where they're they realize that stuff moves so fast that everything is invisible effectively from the volume. And so you have to be extremely loud and transparent and intentional about saying everything that you're doing so that if anybody else is doing it, they can stop you right then and if they need to integrate with you, they can start right there.

**1:14:47** · And and we're talking about startups that that are looking for product fit. They're looking for customers. They actually just want to get that what we call product market fit where the traditional wisdom was build something amazing and then release it to the world.

**1:14:58** · Right.

**1:14:58** · That's right. Try to find product market fit in secret as much as you can and then launch it and and then and then tune. Right. That's that's that's the formula and many people failed at it.

**1:15:08** · It used to be now like you're saying with Gas Town I I I realized I'm not going to find product market fit by myself. So I launched it as soon as it kind of worked and was like help me and that's how I found out about the adult database which was a big change and and people people fixed a bunch of bugs. I got 100 plus PRs the first couple days and right and so it found its way closer to product market fit just by me getting it out there.

**1:15:29** · And would you say that has brought you like on one end people look at you well yeah it's just one other open source project but is it bringing actually opportunity if you wanted to could you turn this into a business has it has it brought you the things the where I'm getting at is is these things that take off those open source projects like can they actually turn into actual businesses are at that stage I promise you if if you had made Gas Town you would be you would be shaking venture capitalists off you like ticks right now I am they're They're they're they're they're finding me everywhere.

**1:16:01** · Okay. And and I and I and I tell you it's because there's a lot of money out there right now sniffing wanting to find its way into a it knows something big's going to happen, right? And it's looking and you can see it in all these different microeconomies that are springing up. But nowhere can you see it more clearly than when you launch something cool like Jeff Huntley did Ralph Wiggum VCs, right? You know, everyone want to talk to him.

**1:16:23** · You just got to be real careful because anything you build probably has a real short shelf life at this point, right? a real short one. I don't I'm not attached to Gas Town in any way because I think it'll be supplanted by something better within six months if not sooner. Right?

**1:16:36** · So too attached.

**1:16:38** · So let's assume that staff engineer is listening to this podcast or watching it on their commute and they're at the type of company where they have co-pilot still there's people like this and and they're using it and they're they're they want to believe you but they're not sure they can. What would you tell them?

**1:16:53** · what is the the thing that they can do to get proof that you're actually right and this thing is is working. We're not at 100%. We're not even at 50% for for people like a lot of people who are in this field have tried it out but there's there's a lot of people I would say probably still 70% aren't aren't doing it. Yeah.

**1:17:10** · Um so like what would I say I had a really good message for them. Oh yeah.

**1:17:14** · Get out. Get out. Um, so here's the thing, right? Copilot is uh if you were to line up all the tools, you know, from best to worst, right? Copilot is like here a line, right? It doesn't even know about the line, right?

**1:17:29** · But it used to be the best four years ago in 2021, right?

**1:17:31** · Yeah.

**1:17:31** · And I was competition even maybe two and a half years ago, I was quite stunned that uh that somebody asked, "Does anybody use co-pilot at an AI tinkerers meeting?" And and somebody raised their hand. He goes, "Do you have to?" And everyone laughed and I was like, "What happened?" Right? The brand just tanked. But I'm serious. If you're working at a company that uses that gave you co-pilot, they think that they're starting to move faster and there's a barbarian horde of people using Opus 4.5 that are destroy your company sooner or later.

**1:18:00** · So what you need to do is go into the crazy part of crazy town and figure this stuff out and start building. hand because we are moving into a world very quickly this year where proof of work is so important and I mean proof of work not in the Bitcoin sense but your proof of what you have done your resume and I don't mean your resume because nobody's going to believe that I mean the actual work that you did which has to be visible back to our transparency right I

**1:18:26** · think everyone's going to be bringing their work with them I mean the notion of proprietary work is starting to like be threatened I think because it's so easy to fork it's so easy to clone it's so easy to route around if you have anything proprietary you become this this thing that everybody just wants to run around you and so right so big big changes are a foot but man if you're working with co-pilot right now you are going to get left behind and so what you need to do is get get yourself find a half an hour a day to go play with with cloud code right and uh and

**1:18:57** · and and and it's like I said or if you're a company make your token burn as high as your investors will let you go right because that token burn is your practice it's your it's your sorting things out.

**1:19:09** · So I I want to ask you the other way around. Let's assume you're just wrong in terms of the the curve and we're we're at the peak and it will not be 10x, it will plateau at 3x or let's just say the next model is inexplicably dumber than Opus 5 we've peaked.

**1:19:26** · What would happen to the person who takes your advice and they go all in and they learn things? What's the worst thing that could happen to them? If you know if if these things take off, it's a great investment, right? But but what would happen to them if if they followed your advice and the models didn't follow. Where would that leave them?

**1:19:41** · Exactly

**1:19:41** · where they need to go because the damage is done. Opus 4.5 made this officially an engineering problem. We don't need you AI researchers anymore. Thank you. You can make smarter models, I guess. But we don't need them because we have something can you can take a bite-sized chunk out of a mountain and it's a bite size about town size now.

**1:20:00** · And so we can eat mountains. Okay. It's purely an engineering problem at this point. It's like fire or steam. It's a it's a force. It's a power. And we wrap layer layer layer layer. I worked on a nuclear reactor. I was in the Navy. I know how these things work. Okay. We are going to put all right uh layers around Opus 4.5 if that's the smartest model ever. And that will do all of the engineering from now on. So, it's done.

**1:20:23** · So, it's okay to jump into the pool.

**1:20:25** · Now, your first job was about debuggers or or not debuggers, but you worked at this amazing company. You told me they had the best debugger tools. What was the name?

**1:20:33** · It was GeoWorks and the debugger was called SWAT and it was amazing time machine and all that and and on the first pragmatic engineer interview when we talked uh this is in the newsletter you actually saying that you to this date you've not seen as good of a debugger but you're kind of determined to like build at some point and help build that.

**1:20:50** · I did build a debugger enclosure for the JVM called Ganja. It was actually pretty cool but then I got an argument with Rich Hickey about how well he wanted to support the JVM and he doesn't. So um yeah but anyway you you're a guy who who is passionate about about story somewhere though.

**1:21:05** · Yeah \[laughter\] you're passionate about debugging. What will happen with debugging? What will happen with debugging tooling? What do you think the future of debugging is?

**1:21:14** · Uh with agents when I see agents say I'm going to debug this. They all use printfs. So uh you know I'm curious. It could very well be that they just haven't been trained on debuggers yet and that they'll all wake up in six months and go, "Oh, I should have been using this." But it could also be that we don't need them anymore. I don't know.

**1:21:33** · And another step further, what do you think the future of the developer workstation like our our rigs, our machines will be, right? Like do you think it'll phone?

**1:21:42** · I want gas on my phone. I almost I have it, but I just haven't worked on it. But Peter Shamberger told me that he had VIP tunnel where you could do it from your phone. He said he stopped it because it became too addictive. Oh yeah, no tail scale. And yeah, actually the only thing that's keeping me from just being addicted to it all day long is it's too hard to enter control characters in, but that's going to get fixed at some point.

**1:22:00** · Programming on your phone will be a thing.

**1:22:02** · But but so do you think that developer workstations can be this lightweight Chromebook, whatnot, or we actually want beefy ones which can run our local agents, whatnot, like where do you think it'll be headed on the short term and then maybe on the longer term?

**1:22:15** · Yeah.

**1:22:15** · See what I mean? Local models.

**1:22:17** · Yeah.

**1:22:17** · No, I um look uh I I love my laptop. I've been programming 40 years.

**1:22:22** · I I get the local thing, but uh I've been saying for at least 15 years that we don't need this stuff locally, right?

**1:22:27** · Google had an amazing client in the cloud high-speed network connection and what you can do, right?

**1:22:33** · City was the base and then Cider was built way up on a higher layer, but but when you get something like that and you're not restrained by the especially in a world where you can run kind of unlimited agents based on your pocketbook, uh yeah, people are not going to be want working on their laptops. And I've already Gas Town has already completely stressed out my laptop to the wire, you know, cuz cloud code actually takes quite a bit of memory. And so yeah, I think we're moving to a world where uh people will work on servers and and and on mobile devices probably less less and iPads, not on um laptops as much.

**1:23:03** · In the past, you've said that one of the most important kind of predictors of develop productivity is language design. Well-designed languages are easier to work with. Do you think this has completely erased or do you think it might come back at some point? either purpose-built languages.

### Where languages stand

**1:23:17** · I think there will probably be purpose-built languages by AIS for AIS maybe, but right now we're in a funny place where the some languages work better than others still because they have better training data. But in the fullness of time, all the languages will work equally well. Uh I'd push back on that like if if a new language never has training data, how would it work that?

**1:23:37** · No, I mean sorry, all the existing ones. Typescript, it struggles with TypeScript today. Yeah, it it does, but it's not going to in one or two model really matter.

**1:23:45** · So, could we see a stagnation just fewer languages or no languages launching because they just get the job done and launching a new language seems a bit suicidal unless you like bring a bunch of like training data with it, right?

**1:23:55** · Man, that's a loaded question. I mean, like part of me I didn't mean to make it loaded.

**1:24:00** · No, it's a good question, right? Part of me says like languages just don't matter anymore, right? any more than assembly languages matter except for a few people who are trying to optimize really important things and then everybody else it doesn't it just doesn't matter right but then part of me says well energy is the most constrained and important resource on this planet and it's only going to get worse so finding better algorithms finding better ways to solve problems is often a language problem finding a DSL you know so I think for an

**1:24:30** · optim from an optimization perspective an efficiency perspective the search for new languages will probably you but for pragmatic for for everyday I don't think it it doesn't matter what you pick you might not even ask your your agent what language it's using \[laughter\] so as a software professional who like loves the crafts is is into you know languages debuggers tooling etc a lot of what we talked about is pretty pretty sad because you know like a lot of the the the beauty the challenges that that we worked it seems they might be going away if we continue and if this continues as well.

### Adapting to change

**1:25:00** · How did you work through this yourself? And and also what is what is the thing that actually excites you looking ahead?

**1:25:09** · Right.

**1:25:09** · So I had the benefit of going through 30 years of graphics evolution.

**1:25:14** · And so I saw the sadness and I saw the resulting much better games we got after all that happy stuff we were doing by hand moved into the hardware. We're sad because we're used to it. Change is part of life. Okay? And we're, you know, at one point I had to say goodbye to assembly language, right? I was like, compiler writers, they finally caught up, right? And then we were mad, but then we were happier because compilers are obviously way better than writing an assembly language. And anybody would be stupid to say, oh god, yeah. No, you're not a good engineer if you can't write an assembly language today.

**1:25:44** · But that was actually what we were saying in 1992.

**1:25:47** · Yeah. And then you had the blog post out in in 2012 as well. Yeah.

**1:25:50** · Yeah.

**1:25:50** · No, I'm just saying stuff changes.

**1:25:52** · What you need to know as an engineer will change and you can't rest on your laurels. and we're going through a period of faster change now.

**1:25:58** · Mhm.

**1:25:58** · But you have helpers called agents that can actually help you through this change. So stop complaining and just go do it.

**1:26:05** · Yeah.

**1:26:05** · And I think just recognize we're in this industry where change is a thing. And that's right. Now with that said, go through the five phases of grief, right?

**1:26:12** · The five stages of grief. I mean like I went through uh I don't know if I I don't know about anger. I was angry. I was really angry for a lot of reasons two years ago. But but no, I mean like if you've ever truly grieved, if you've like lost someone, you know that it hits you in a lot of weird ways where you feel reality disconnected. Uh you feel uh sick, you feel stunned, you feel all day long, the world goes monochrome, all color disappears, all kind of weird stuff, right? And I went through that for about I don't know six or seven days. It didn't take me that long to get through it fortunately.

**1:26:41** · Or maybe it was that was the peak and I was it was surrounded by a few months of it on either side. But there was a period that I went through it where I was checking off things that no longer mattered that I had really cared about like my ability to memorize or my ability to write or my ability to compute or whatever all those anything computing related I was very sad right because those things made me

**1:27:05** · special somehow right but then to your question what makes me excited like as soon as I got through that I was like but wait I'm writing 10 times more code than I ever was and I'm having fun and why should I be sad this right and So, I realized it's just it's just me holding on to the old just like I did in graphics. And there's no point because the future is actually more fun than the present. It just it's going to be.

**1:27:26** · You're known for your predictions and I'd like to put it to a test. Let's give some specific predictions for for next year in 2027. Things that you think will happen either with how we develop or or how the industry works.

### Steve’s predictions

**1:27:38** · I think that my wife is going to be the top contributor to our video game.

**1:27:42** · Oo, bold claim. summer of next year.

**1:27:45** · And she is not a developer, I'm guessing.

**1:27:47** · No. Oh, no, no, no. But she loves our game and she has lots of ideas, right?

**1:27:53** · Amazing.

**1:27:54** · Yeah.

**1:27:54** · In fact, I think my whole family might be in on it. I I'm serious, man.

**1:27:58** · Programming is going to be for everybody and it's going to be the most amazing thing because you know how much fun we've been having all those years and we've been telling people it's really fun, but now they're going to get to experience it, right?

**1:28:07** · I I look at my kids and how they look at AI. They're having so much fun with it creating. They're just prompting Gemini or or any of these with their imagination and they actually have they don't think it's weird. I I think it's weird so I never would think of it, but they just enhance our photos with like squirrels on my head and it it it just made me laugh and and fun and you realize like there's just a lot of fun and new things with it when when you let go or or you never knew what was before.

**1:28:33** · It's given the people the ability to do very sophisticated mashups of anything. And mashups are really where innovation happens, right? Innovation comes from taking things and putting them together and seeing where it goes, right? We're going to see everybody innovating, man.

**1:28:45** · And it's going to be the most amazing thing ever. And then we're going to need ecosystems of agents that can go find stuff that you like because there'll be so much content. How are you going to find the stuff that's really like that you like? You're going to have an agent that knows you really well. I think any software engineer who wants to get go make a big business right now should go start working on agents that know how to go and search the new world, everything that's coming. I what we call it, right?

**1:29:09** · the work pile for for uh software that you like, for experiences that you like. And if everybody's creating it, think about it. When when the internet came out and everybody could make a web page and upload we needed aggregators.

**1:29:23** · We needed, you know, we needed search engines. We needed ways to organize and find and surface the good stuff, right?

**1:29:30** · None of that exists right now, but everybody's about to start coding like, right? You know, and so like you can get ahead of this. This is why I keep saying just believe the curves. pick a point on the curve and aim for it and you will land there and you'll be first when it when when the AIs are ready for your thing.

**1:29:45** · Yeah. And I think as engineers we already can build. We don't need permission. We can use these tools super efficiently right now.

**1:29:51** · And we are ahead of we are ahead of the rest of the world right now.

**1:29:54** · Right now.

**1:29:55** · Well, it's exciting times. Well, Steve, we'll have to check back on on how if if if that prediction will come through with your wife contributing more, but this has been I think really eye opening and and it's, you know, sometime I think it's good to to go through the has been and the can be.

**1:30:10** · Yeah.

**1:30:10** · Well, thanks. I hope you enjoyed this \[music\] conversation as much as I did. An interesting thought from Steve is his parallel between the graphics industry and what's happening in software engineering right now. In 1992, Steve was learning to calculate where individual pixels \[music\] go on a line.

**1:30:27** · Two years later, the same course was teaching animation. The work in graphics went from writing \[music\] device drivers to building game worlds and physics engines. It all just moved up the abstraction layer. Steve's argument is that software \[music\] engineering is going through exactly that same shift right now, except it's faster. Instead of asking, will engineers have jobs at all? A better question might be, what will the new jobs we do as software engineers look like? Another thing was the grief of this change. Steve is someone \[music\] who spent 40 years building his identity around compilers, debuggers, elegant code.

**1:30:55** · And then one day he sat down and started checking off one by one the things that made him special that no longer mattered. His world went monochrome as he said. Within a week or so he came out from the other side and realized he was writing 10 times more code and that he \[music\] was having more fun doing it. Still, I think a lot of engineers are quietly going through something similar right now and it's usually taking longer than a week to digest all of this. Finally, one thing I found really honest from Steve was his point about value capture.

**1:31:25** · \[music\] If you become 100 times more productive with AI, who benefits? If you work 8 hours and produce 100 \[music\] times the output, the company captured all of that. But if you just work 10 minutes in a day and produce the same value as before, \[music\] you technically captured all of it and your company captured none of it. Now, neither extreme is sustainable. Steve is saying that this new work life balance is a question that we'll need to figure out.

**1:31:46** · We don't have the cultural norms for any \[music\] of this and it's going to be messy as we figure it out. If you've enjoyed this podcast, please do subscribe on your favorite podcast platform and on YouTube. A special thank you if you also leave a rating for the show. Thanks and see you in the next