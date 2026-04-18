---
title: "Lessons from building Vercel v0 and the d0 agent - The Pragmatic Summit"
source: "https://www.youtube.com/watch?v=_f2WpsmW76Y"
author:
  - "[[The Pragmatic Engineer]]"
published: 2026-03-06
created: 2026-04-18
description: "With Malte Ubl (CTO) at Vercel. Recorded at The Pragmatic Summit www.pragmaticsummit.comWatch the session with Q&A also included: https://newsletter.pragmaticengineer.com/p/the-pragmatic-summit-reco"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=_f2WpsmW76Y)

With Malte Ubl (CTO) at Vercel. Recorded at The Pragmatic Summit www.pragmaticsummit.com  
  
Watch the session with Q&A also included: https://newsletter.pragmaticengineer.com/p/the-pragmatic-summit-recordings  
  
0:00 Intro  
2:19 Rebuilding the agent stack  
12:22 Business users shipping apps  
20:05 Reliability architecture  
25:58 Org evolution

## Transcript

### Intro

**0:04** · Malta, thanks for having the conversation with us today.

**0:09** · Um, this time it feels different when it comes to coding agents. I think there have been times in the past where, you know, it it felt like it was uh a little revolutionary, but I think this time we're all trying to figure out how we are supposed to build while the ground underneath us is shifting. And so super happy to be speaking with you today.

**0:33** · I think that with your products uh DZ your internal data agent and then Verscell V0 as well your public facing thing um you've you've been able to roll with the punches and and be able to build and and create products as the world has changed around us. Let's start with DZ your internal uh data agent. What was your first approach there and why did it turn out to be so flawed?

**1:08** · Yeah, to give folks a little bit of context like the thing that makes Versell strong is that we always build things with our own technology and like one of our thesis is that like building agents actually extremely easy and you don't need to buy them. You can just build them yourself. And so we build one ourselves and so the the agent that we call DZero internally is a is a text of SQL engine. So you you give it any question in Slack and it will reply with the answer and it has access to our entire snowflake kind of subject to the to the access rules of the of the user.

**1:41** · Right? And so um I I'll share one query which I think is the funniest one. It's a salesperson. You'll hate it all. Um so this early this year they um this person asked the following question. uh which S&amp;P 500 CTOs and VPs of engineering have private Versel accounts and have deployed over Christmas.

**2:03** · So presumably they got like an email or a call. I don't know. But like I think like that's like if like actually finding that from I mean obviously you have to do a little bit of research. You have to go to LinkedIn etc. The agent does as well but then eventually you kind of figure out the right snowflake query. It's it's very very difficult right? Um, and so the the initial version of this agent was kind of this kind of traditional infrastructure where you have, you know, the agent is a tools in a loop type of thing. Has all kinds of different tools to do all kinds of different things.

### Rebuilding the agent stack

**2:29** · Um, and it wasn't like it was working badly, but it was, you know, maybe not as magical. And then we deleted everything and switched to like an agent that looks very similar to a coding agent. Now it's it's it's still kind of custom coded like it doesn't use for example cloud code as a harness uh because again building such a harness is actually really easy and you can just do it. Um but otherwise it kind of looks the same way.

**2:56** · So the the the general architecture is that we did the work of going through our entire snowflake and for every single column in pros explaining the business value, right? And that gets exported to a YAML file. And the the agent essentially gets told, you know, you got post-trained on using GP on tail and and all these things, right, that you need for coding and go to go to town on these YAML files to figure out the business semantics of everything.

**3:28** · And then you make a SQL query. Um, for that it has a completely different custom tool and that's it. So there's just two tools. There's the bash tool and there's the SQL execute SQL tool. and and that's the entire agent. So, it has like 50 lines of code. Um and and it's completely transformational for the business.

**3:48** · What led you to understand that you needed to throw everything away? Cuz I feel like you go and you build all of this this code and it's it's just so hard to light it on fire and then start from from scratch again.

**4:02** · Yeah.

**4:02** · I think like I think in the in the world of agents, you have to be humble in the sense of like we're just discovering how to build them. And so just because something was best practice like in the summer of 2025 means quite little today and like that's different from like I don't know if you've built a website you know it's been 30 years and we kind of know how to do it but on you know agents are in their maybe third year for real if at all right um and so

**4:31** · you have to be willing to entertain the notion that yeah maybe there's actually now a better way to do it and like it's kind of proportional to the models getting more intelligent so you And it's more viable now to have agents that are essentially it's fully relying on the emergent behavior and and respectively um are more simple because you don't have to prompt them so much. You don't have to hard code so many rules.

**4:54** · Uh on the Verscell blog you had a uh a post it was titled I think all you need is the file system in bash. Is that is something like that? And so you just took a complete step backwards and and described what the the data was in in plain English and sort of like you just step back and let it cook and and move to a much more declarative model with everything, right? Yeah.

**5:21** · The intuition is that you kind of you have to think about like what was the model trained on like what what what is it optimized on? And for now there's lots of coding tasks, right?

**5:32** · And it'll change in the future. And so if you can make things look like like they're a coding task even though they're not um then you can uh you have you get disproportional good results.

**5:45** · How many CEOs and CTOs in the the Fortune 500 are using Versell on their personal accounts?

**5:51** · I I don't have the precise number. It was pretty substantial.

**5:53** · Okay.

**5:54** · Yeah.

**5:55** · Dozens of them.

**5:57** · Well, I just it is it's quite amazing now to see all of these CEOs and CTO's come out of the woodwork and start coding and and doing all these agents.

**6:06** · Are are you one of those CTOs that are close to the ground and and shipping stuff?

**6:11** · I was already before, but I'm I'm deep in 12 hours a day coding. And by coding, I mean like I I can do meetings, right?

**6:20** · cuz I can, you know, just kind of every so often uh optimize the I go in, check the prompts, deliver a code review. Yeah, I'm super back. Uh I I've been for for the longest time kind of oscillating between coding a lot and and not coding so much and I'm I'm back on um like 24/7.

**6:38** · What's what's your drug of choice? Your agent of choice.

**6:42** · So for I mean for Versell, we try for folks to get a broad experience across the company. We want to feel what our users feel. So we want to we don't we don't mandate anything. Um my current stack but it's subject to change is uh clot with 4.6 fast and then I'm using uh codeex 5.3 for code reviews.

**7:02** · Yeah.

**7:02** · Yeah. It's uh it's quite amazing.

**7:06** · It's just this like dopamine hit where you're you're uh you're hitting the the slot machine hoping that you get something awesome out of it.

**7:13** · Right.

**7:13** · Like that. By the way, I had u there was an article in Wall Street Journey journal of me basically saying that and so that was my first ever quote in a major newspaper. Here you go.

**7:22** · Oh okay.

**7:23** · Oh wow. We both came to that.

**7:25** · So voted to be addicted. But yeah I'm I I maybe I'm not addicted but I do love it. It's such a good experience.

**7:34** · Well let's shift to Verscell Vzero uh which I think you launched back in 2023.

**7:40** · Is that correct? Yeah. So the original pitch was um anybody should be able to make an application even non-engineers and you could do some prototyping and stuff like that which was I think pretty revolutionary at the time. What did you think Vzero was going to be and how quickly did it start diverging from the plan?

**8:03** · Yeah, I think initially we we thought we were building a tool for front-end engineers uh because that's what we're doing in general, right? And so like we we thinking we were making a tool for ourselves and we then realized we actually built a tool for backend engineers because it was empowering them but it also sucked um in the sense that it didn't work all the time.

**8:24** · And you know this is 2023 GPD 3.5 GPD4 days and so it didn't work all the time but the back end engineers they were good enough to fix it in the cases where it didn't work but you couldn't have given it to a non-engineer at the time right because it was just not um reliable enough and and so that was the that was the kind of the main part of market fit for a while and then uh we

**8:46** · but again in the AI space you have to be humble right like you have to be willing to entertain that the world is changing around you so sometimes people call it a pivot but it's It's not really the right word because usually that's used for the cases where you realize that you kind of made a mistake on your internal data and you have to do something else. Whereas let's say anthropic ships sonnet 3.5 and suddenly essentially the same prompt can be used to build full stack apps which previously just wasn't possible. You cannot now keep your product the same because the world is different, right?

**9:16** · Um and so that that was like a major milestone where like we we realized okay we have to um and I mean obviously this amazing right like we can we can now h uh adopt our product to be able to build like end to-end applications and also with a success rate that kind of approach is the the case where um where a non-engineer can be successful.

**9:37** · So you told me there were about five oh moments when it came to vzero um over the years where the models took a really big step forward or you know usage patterns shifted and you needed to rethink things. Can you take us through one of one or two of those moments and and how you were sort of thinking about things? Yeah, I mean definitely the first one was um like in the summer of 2023 when um to take us all back, right?

**10:08** · The CHBT had launched and LMS were still kind of new and and and broad adoption and these things were making text and so I think us and everyone was thinking like we got to like it must be possible to make web pages with these things and back in the day when you tried you would realize that it wouldn't do a good job.

**10:29** · uh like it would kind of do it but like it wouldn't look good. It would kind of be be um be subpar. Not something you would package as a product. And I still remember to this day sitting at the like we had like someone actually who who is from China and lives in Berlin, but he was in our office in San Francisco and he was hacking away and then at some point he was like raising his hand like guys I've I found something. And so he had just changed the prompt to say use Tailwind.

**10:58** · And this was such a like serendipity moment because Tailwind at the time which is it's like a way to write CSS um at the time it was old enough that it was in the CHBT 3.5 um training kickoff.

**11:09** · Um but at the I mean at that time it wasn't super popular yet but it was enough training data and so the model is so much better at doing inline reasoning rather than saying we have to write a CSS file then later write CS HTML. the models at the time were too dumb to do that. So they so they couldn't, right?

**11:25** · But if you if you told them basically just put everything in the same place, then they did a real job. And so that's kind of how we figure out how to build a product that actually was viable back in the day, right? Um so that that was the kind of the first milestone to actually make it work. Um eventually like I mean

**11:41** · I already mentioned that we like the second really big pivot was was that um I think the the the final step you know obviously there was like this whole ecosystem now of of products kind of in this space and and some of them went very much like into the consumer space um and and we definitely discovered okay

**12:01** · there's this like enterprise use case so like when for vzero the the users we're aiming for I would call tech adjacent right so it's the it's the PM, it's the designer, it's the the product owner, the the business person who's kind of interested. It's like um that found the law of product market fit. Um and then the final use case, and I'd love to talk a little bit more about that, but like that is essentially um I'm a I'm a business person at a company.

### Business users shipping apps

**12:26** · I'm going to make an internal app for myself, right? um kind of the new like crazy onslaught of of shadow IT um is definitely something that that we're very interested in both from a from a from the VCR point of view but also from the Versel deployment point of view.

**12:44** · How do you think about um how do you think about the fact that the models are so fully capable right now and like where does Verscell sit in uh as a product, you know, as these models get better and better?

**13:03** · Yeah.

**13:03** · So, we're we're a multi-product company, but like so our core business for folks who don't know is you throw over the fence and we're going to run it for you. Um, and the the beauty of that is that there's no more being made right now. Sorry for cursing on TV, but here we go.

**13:19** · Um, so like like like every like we love it if you use cloud code, if you use cursor, you know, like if at some point you're going to have to have a place to run it and and um you know, we can connect Versell to your git repository and every time you push um we'll make you uh a new version of it and have it in production. So, so that's kind of like that's how I see my primary position in that marketplace, right?

**13:42** · And then, you know, with VZero, for example, obviously you're also playing kind of on the creation side, but I certainly spend most of my time actually on the the question of how do I run these apps that are made in a different way in production in a way that's um like that's appropriate for this new type of application.

**14:03** · So on a scale of 1 to 10, as the CTO of a tech company in 2026, how worried are you that the stuff that you've built will become obsolete as these models get better and better?

**14:20** · There's things I'm worried about. Um, but I don't really see like uh like again like you know since we're in the business of operating software um I don't see a major disruption there. Like you could argue, you know, the agents are also great at writing Terraform, like you know, they can just make the infrastructure for you, but like that's actually not how that works, right? like the the the whole idea of of of any form

**14:51** · of professional DevOps is that I have like somewhat an idea of what's going on and and so I can't like you can't really vibe code that like you you so you there has to be there always has to be some form of platformization of how I run something and um and so that like you know essentially we're playing in that in that space relatively successfully. So for that from that point of view I'm actually not particularly worried.

**15:17** · Well, do you think that the lack of observability is a temporary limitation or a fundamental limitation of long-running agents?

**15:30** · Like uh you know I think that the the there's there's a whole you know there's a whole revolution ahead of us of of agents participating further in in kind of the DevOps space and and and and running your application. um we started calling it kind of self-driving um like infrastructure where like where the you know where you have essentially something that in an agentic way kind of understands what's going on.

**15:57** · Um but yeah I think that still kind of like relies on the fact that there is a certain uniformity how how things are running versus essentially you know let letting the AI kind of loose.

**16:11** · If you were to start the Vzero team today from zero, how would you do it differently than when you started it in 23?

**16:23** · Oh, that's a really good question. I I think the the obviously now we under like if you already know what what the product market fit is, you can jump over all these steps, right? Um I think the the big difference is that today you actually don't need a team. Like so if you start why would you have a team?

**16:42** · Teams just I don't know make things go slower, right? Like you can you can always go to the step where like where you where you have enough that you can make a judgment call as to what whether that's worth investing with a single person. And maybe there's two of them.

**17:01** · Maybe there's three of them, right? But it's not like seven people, right? And so I would I would tell someone, "Go figure out what the product is and give me a demo and if the demo is good, I'm going to give you a team."

**17:16** · So you would just have one dude like just go and do it after you found the market fit or Gallop. But yeah.

**17:21** · Yeah.

**17:21** · Yeah. Yeah. That's amazing. Um so how are you thinking about your dev teams within Versel then? Are they much more about like one person and and one sphere of ownership and then they go and they do everything or are you trying to retrofit maybe like a broader team dynamic?

**17:47** · I don't I definitely don't think we have like in a major way kind of changed how how how we operate. Um, I think it was always a good idea to have individuals to be able to ship something end to end and and to not really always rely on the entire operation to make progress. And I think that's kind of like many of these many of these things, you know, continue to be true, but they're they're probably more painful now if you if uh if you if

**18:14** · you you know increase the speed of the inner loop through a coding, but your outer loop of shipping is uh is different. Um I give you one example which I think is relevant for this group. Um so I I was at Google before for 12 years. I led like part of the search team. Um you can imagine essentially being a very slow oper operation, right? Uh my job was essentially to approve things via email and go to meetings. Um and so I didn't want to build the organization.

**18:39** · And so the the the pattern that we use at Verscell is what in the nerdiest way you could describe as optimistic locking. So there are no approvals.

**18:54** · Um anyone can ship anything but they have to tell the organization that they're going to do it and the organization can veto things. And so vetos actually kind of sounds scary and weird but it's really empowering, right?

**19:10** · Right? Like if the legal team, they says like like most of the time they say, "Yeah, I mean this sounds totally reasonable. I don't need to spend any time on it." Right? But sometimes they'll say, "Oh my god, you cannot ship this to like children in North Korea."

**19:22** · Um like there there's a there's a like, you know, sometimes that's true, right?

**19:26** · But uh um but if you have a process where legal has to say yes, uh then you have to wait for them and like there's this round trips and they're on vacation and like whatever, right? It's it's it's complicated if you say well no you can always say this is not okay but you have to you know do you have to now be an active actor in this process you kind of it's both empowering for the for those teams but also puts the the responsibility well that's interesting and so

**20:01** · like you guys are like ultimately you're an infrastructure and devops corporation how do you see the role of like reli iability and maybe moving a little bit slowly and and more conservatively for the uptime of all of your customers versus like wanting to move really quickly in this age of agentic coding.

### Reliability architecture

**20:21** · Yeah, I think the the it's it's just not right to take those things to be in opposition.

**20:28** · But like essentially everything like everything we do in our business um and we we have this like kind of maybe great situation where like it's our business to make our customers move fast and we're taking advantage of it ourselves, right? We're own first customers. And so everything I do is I think about how can I make my teams move faster? Um how can I, you know, improve the speed of the inner loops? How can I improve the speed of the of the outer loops of shipping?

**20:56** · And so like if I uh like that doesn't mean I never make a trade-off, right? Like for example, we only ship our um like serving systems once a day, right? Um whereas we ship our control plane every time time someone pushes to to main. And so would I love to be able to, you know, make a new feature in our um consumer serving stack on a like 15 times a day? Yes.

**21:23** · But you know we did make some trade-offs there. So obviously there's you make some decisions but it doesn't mean that in in like that you cannot move fast and uh you know not break things right like there is it's possible.

**21:39** · Well you know um I did a deep dive into Cloudflare's outage and it turns out that it was some bad data in the control plane twice. Um and uh the whole reason they had the dynamic configuration was that they could move really quickly and make changes and customers would see that reflected really quickly. But you know this globalized like key value pair store that is storing these configurations has the potential to take out 20% of the internet.

**22:08** · And so do you make a distinction between the ops and the devops part side of the corporation and then the the software and the engineering and the architecture? Are those the same thing? No, it's a really good question. I think the like also from my experience at Google like every time Google goes down which you know at at a at a large scale only happens maybe like every five years, right? Every single time there's it's one of two things.

**22:33** · It's either like a bad config change or it is like something around the like like secrets management service that everything depends on, right? or it's a config change of the secrets management service which I think was the last big one. Right. Right. So it's it's always going to be that.

**22:51** · Um and so I mean in Verscell's architecture we uh so we operate 20 regions 20 core regions and so on the serving stack again we we have deliberately decided that we want these regions to be autonomous and we don't have a mechanism to change them all at once and so we uh

**23:18** · we thankfully cannot do these type of confict changes that break everything at once and so we we change them in waves and so yeah there's another like kind of deliberate decision to say okay we um if I want to move fast I want to be able to get get relatively quick feedback on my config changes right let's say feature flex for example and so but for that

**23:40** · like to get that feedback you actually don't have to ship it globally right it's completely sufficient to say um you know maybe I only put it into one region and see what happens Um and then obviously when that region goes down we can easily just take it out of the rotation. And so like you can I think every time you you do something it's obviously important to think about like what is the what's the risk profile and can I find a way to make essentially

**24:07** · progress at the same velocity but without taking down the risk of for example global outages of 20% of the internet.

**24:15** · Are you one of these shops that give unlimited tokens to your devs?

**24:20** · Absolutely. We even put it into our uh job description on I I could not see why I could possibly not want that. I mean, obviously people, you know, there's always going to be people who abuse some policy, but like I mean, how much could it be?

**24:38** · I don't know. You're the CTO. Don't you know about your cost?

**24:40** · No, we had a guys like basically people like mostly it's it's bucks, right? Like I had a engineer who was 10x the second one was like first of all I was impressed. Um, second of all, we found out that his um custommade coding harness uh had like was changing the prefix of the prompt so that it wasn't hitting the caching um system and so which is drastically more expensive, right? Um so obviously it happens but yeah I think it's worth having an eye on it but otherwise um I think the the more the marrier.

**25:16** · Are your code changes uh going into production? The CEO's code changes, are they going into production?

**25:23** · Uh so my CEO I think still deploys an app to Versell every day. Um but he very very rarely does production code changes. And I do I mean regular about you know maybe two three times a week.

**25:42** · Okay.

**25:43** · Nothing nothing super big. Um, I think it's a really common profile people in the room will have where you say, "I do things, but not the ones that actually are important."

**25:54** · What do you think the future of your tech organization is going to look like as these agentic tools just get more and more powerful?

### Org evolution

**26:07** · I think what's already happening is that there is like the job is just looks much more like management than it looks like I see work and that I think does kind of change a

**26:23** · lot about the profile of the of the people and so we what we see is that um the the most senior IC's are in a way the one that benefit the post because they're they kind of already did a very similar job, but now they have just more minions. Um, and then and then the other folks who benefit the most are the the most junior engineers. Um, because they for the same reason that they're better at making Tik Tok videos than me, right?

**26:55** · Like they're growing up with that stuff. Um, I think what what's most interesting is kind of what happens in the in the middle. um like where people have to still learn to be in this in a way new role and also have a kind of a um you know or need to be just willing to engage with the technology.

**27:20** · So are you one of these companies that's really leaning heavily into interns and junior engineers?

**27:27** · Yeah, we I mean I I I'm year over year very very impressed with the internship program. Um and yeah, we also have um like a pretty very very decent cohort of junior engineers.

**27:43** · So in terms of your organization, what does it look like in a year? What does it look like in two years?

**27:52** · Obviously, I don't know. Um my my CEO and I have this quasi joke that we So right now we're like 750 people and we just quote unquote decided that we cap employee count at 1,024.

**28:10** · Nice round number.

**28:12** · Um which which is notably below our hiring plans for this year. Um so we'll we'll see what actually happens. Um but so I I I I could see right that there's essentially this asmtote right where like you know you you grow the company but at some like the the growth kind of even let's hopefully our growth as a as on the revenue side kind of keeps growing up but that maybe you you actually don't need more people. Uh I is it realistic?

**28:46** · uh like I it's like we we I mean we so we see agentic transformation obviously on the coding side everyone here does um we automated for example our uh sales leads qualification with an agent that we also open sourced um we automated 87% by now

**29:07** · of our support intake um and that you know that's actually good example for did we let support agent go no A I mean first of all the company's growing fast enough that you know that would never be necessary and B they have a much better job now because they only have to solve the hard problems which I think as a support engine you enjoy more but the um

**29:30** · so I think there are some factors that kind of are you know at least reducing growth and so I do I do think there is going to be a transformation on that on that line otherwise my like the real journey that I we're all on is that we're figuring out how elastic the software market is, right? because we are making it cheaper to make software and the like what's

**29:57** · definitely true and I think we're very much seeing this also in our own numbers is that leads to more software and and so you like the question is like you know obviously that's going to balance out at some point on some equilibrium and it's completely unclear to me right now if that equilibrium has more software engineers than today or fewer but it's very possible that it's power.

**30:20** · Um, and it's also very possible it's fewer, right? like but but it's I I I I I couldn't tell how because the like the maintenance burden that is associated with all that free free software is very substantial and but also like you know as long as it gains the productivity wins it's not worth investing in it having people who manage it and so forth like yeah I can see how you're positioned to

**30:50** · support all of this new software that's going to be created So I'm pretty bullish on that. But yeah, I just think the the big question about whether we're software light or software heavy in this new world where software is free. I think of it sometimes like like YouTube, right? So you know before it was very very expensive to create a you know TV show or a movie and now anybody can do it. And so turns out we were actually video light in 20 2005 or 2006 when when YouTube came out.

**31:21** · And I do think, you know, nobody knows the future, but um if we are software light, it's going to be pretty great.

**31:31** · That's I love that analogy, right?

**31:33** · That's exactly my point, right? There's going to be more software. And you know, there's now like the number of people that are engaged in professional video production is drastically higher than it was 20 years ago. Um and again like they're they're um that doesn't mean there's no changes, right?

**31:52** · I think when uh like to quote kind of Ben Thompson who I think is making this really good analogy that the transformation is probably closer to the one in the 60s when the main frames were introduced and the buildings full of quote unquote computers um you know no longer had a job. Then it is like the transformation of the introduction of the internet. Um but and so that if you look back at the transformation in the 60s um that was very painful for some folks, right?

**32:23** · But like but overall from a from a societal perspective obviously everyone's drastically richer now. Um so in the long term it goes well and so I think we you know there there's a possibility of of a transformation that's very similar. Last question for me. What's your prediction about the future? That's uh that's a hot take that you haven't shared with anybody else yet.

**32:53** · That's difficult because I tweet everything out immediately.

**32:56** · Oh, okay. Oh, your spiciest tweet then.

**32:59** · Uh I think what I like in my in recent world like I think like definitely um it's certainly the the point is that software you know you already mentioned it's free I mentioned it's free I think we all realize it's free like giving getting a free puppy right like it has to be it

**33:22** · has to be maintained and so I think I mean I'm I'm very excited about the uh the role of agents in software maintenance and exploring that. Um and we touched on like how does stuff happen in production? Uh can I can I automatically maintain something? Um and yeah and I I want to I mean but otherwise I'm I'm just in the same position as everyone like I I now get an engineer saying I build a new file system and they wouldn't have done that before, right?

**33:55** · like it would have been just too much work or like it would have been on the plan that took them six months. Um, but yeah, I don't I know it's not a spicy take, but I really I really want to figure out like what do I do with that file system? Like can I ship it now? Um, or or am I now in a like or or is it actually not real?