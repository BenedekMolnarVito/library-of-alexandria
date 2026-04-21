---
title: "Self-Evolving AI Is Here — And It's Open Weight"
source: "https://www.youtube.com/watch?v=WpcRm78KOvY"
author:
  - "[[Prompt Engineering]]"
published: 2026-03-25
created: 2026-04-21
description: "MiniMax M2.7 is the first model showing real signs of self-evolution — it analyzes its own failures, modifies its harness, and iterates until performance imp..."
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=WpcRm78KOvY)

## Transcript

**0:00** · Can an AI agent train itself? I think we've started seeing some early signs of this.

**0:06** · When OpenAI released GPT-3.5 Codex, they said that this is their first model that was instrumental in creating itself.

**0:14** · There's a project from Andrej Karpathy called Auto Research where the agent performs multiple different experiments and keep those that results in improvements.

**0:23** · But now we have started seeing this in open-source projects as well.

**0:27** · MiniMax recently released M2.7 which is their first model that shows early signs of self-evolution.

**0:36** · Now I want to talk about this model and tell you what exactly this self-evolution means because this is the topic that you're going to be seeing a lot in 2026.

**0:47** · But one quick clarification before that.

**0:50** · M2.7 is not released as an open-source model.

**0:55** · But according to the head of engineering of MiniMax the open weights of M2.7 with an updated versions are coming soon.

**1:04** · So that's why I called it an open weight model. Now before looking at this self- evolution and optimization loop, let's look at some benchmarks. Later I'll also show you some example outputs from this model.

**1:17** · Now let's talk about the benchmarks.

**1:19** · It's on par with some of the closed source models on a number of key benchmarks. However, I would not pay too much attention when it comes to comparison with other models.

**1:30** · What I would recommend paying attention to is to compare this model directly with its previous iteration.

**1:37** · This is where it actually shows substantial improvements on these coding and agentic use case benchmarks.

**1:46** · And you see a huge difference in performance for agentic use cases.

**1:51** · This is where every lab is going. Now we're talking a lot about knowledge work and this is I think where it's going to shine as a co-worker.

**2:03** · There is a very important benchmark called GDP Evolve Artificial Analysis which is their version of OpenAI GDP Evolve data set. And this shows the capability of a model to do knowledge work as a domain expert.

**2:21** · On this benchmark right now, uh MiniMax M2.7 is at fourth position. So if this were to become an open weight model, which hopefully is going to happen in a couple of weeks time, this is going to be the best performing model for knowledge work that is open weight.

**2:42** · Now for knowledge work, you don't only want the model to be great at the tasks that it has seen, but it should be able to learn on the job. And this is where this idea of self-improvement comes into play. Now in most cases in agentic systems, a model is surrounded by its harness. And the harness enables the model to perform actions that are going to be valuable.

**3:07** · Now here's a very simplified version of this self-evolution or autonomous optimization loop. Now for this to work, one of the most important thing is to have a measurable, quantifiable performance metric. And this is something that the model or agent is going to track. So if you run an experiment, in the first step the model analyzes failure trajectories.

**3:33** · That is what exactly went wrong. Then based on that, it is going to plan what to change.

**3:40** · This could be changes to the harness itself. It runs evaluations on the modified code compare the results. It sees whether it got worse or better.

**3:52** · Based on that, it's going to decide whether to keep those changes or revert them.

**3:57** · And then it loops back to step number one. One thing which is very important that I want to point out is that the human in this case is setting the direction or the objective for the system. And then the model is going to modify different hyper parameters of the system in order to improve that specific objective.

**4:18** · Now if you're familiar with evolutionary algorithms like genetic algorithms or swarm optimization, this concept is going to be very familiar to you.

**4:28** · You have an objective function that you want to optimize. The system is going to make changes to its hyper parameters and try to get to an optimization that is going to improve your objective function. That's exactly what Auto Research from Andrej Karpathy does.

**4:46** · This is what GPT-5 Codex did. And this is exactly what MiniMax is doing with their MCDs models.

**4:55** · Now during these experiments, the model was changing the inference parameters such as temperature frequency penalty and presence penalty and also changing its harness by designing more specific workflow guidelines for the models. For example, doing search for bug patterns in other files after a fix. And this led to about 30% improvement on internal eval sets, which is pretty impressive.

**5:24** · Now to show a practical example, they actually have this RL team example experiment workflow in their blog post.

**5:32** · So here's kind of a recreation of that.

**5:35** · Now in this case, the researcher and the agent plan the experiments together.

**5:43** · Then the agent uh basically takes over.

**5:46** · In this case, it pipelines the data, runs the code, logs the metrics.

**5:50** · The agent then analyzes the results, build a dashboard, submit an issue to issues that it finds. In phase four, this is where the human in the loop comes into the picture.

**6:01** · They review the results, discuss next steps, makes the big calls, and the system then loop uh loops back and iterate.

**6:11** · Now all of this is running on top of this harness which M2.7 helped build. Now I think during 2026, this is a trend that we're going to be seeing from every company.

**6:23** · They're going to be building these self-improvement systems which have a human in the loop for critical decision-making. But over time, they're going to potentially become more and more autonomous. But the most important thing is that you need to have some measurable success criteria or verifiable reward even for these supposedly self- improving systems.

**6:49** · Now the result of all this is a very strong model for agentic use cases uh that can do long horizon tasks. Not only that, but I think it's becoming a very good option for knowledge work where you want to use this model as a co-work because of its performance-to-cost ratio. The beauty of this model is that you're getting up to like 80 to 90% of performance of frontier models at a fraction of the cost. So they recently introduced token plans which gives you access to a number of different models with pretty generous rate limits. Now if you want to try out this model, there are a number of different places. They have their own MiniMax agent system which is basically their own harness around the model. Right now M2.7 is available and this is where I highly recommend to test it out. Uh through the API, you can also use this with systems like Open Claw. They even have their own version called Max Claw. Or you can use it with other harnesses like Hermes Agent which is a competitor to Open Claw. Uh it's getting a lot of traction. I'll show you an example later in the video.

**8:06** · So here is one example of the MiniMax agent. I asked it to create a full-stack application where the user can provide text description and it generates images using the Nano Banana image model. Now with within this harness, it's able to self-verify. So it can code, then run the code, look at the output, verify the outputs, and then iterate. I provided my API key as that was needed and it generated this web interface for me.

**8:35** · And then it completely tested the application, made sure everything works, which is pretty neat. Now the app is actually live, but if you look at the output, it's a typical AI-generated web interface.

**8:48** · A majestic lion in savanna at sunset.

**8:52** · So you provide your text prompt, send in the request.

**8:56** · You get the results and then you can just select an image and provide the subsequent prompt to modify the image.

**9:03** · If you want to run this model in other harnesses like Open Claw or Hermes, you will need your own API key. It's a very inexpensive model to run and it's good enough for most tasks.

**9:16** · So you'll need to get the API key from their platform. I am going to try to set this up with Hermes.

**9:23** · So I got the API key. We're going to set it up here.

**9:26** · Now here I switched the model to MiniMax M2.7 and I'm going to run the same prompt through it and see what type of output we get.

**9:35** · So this is exactly the same prompt. All right. So we ran exactly the same prompt that we had before. So this is basically a different harness around the same M2.7 model. All right. So here's the interface created by the Hermes agent with M2.7. Now this is very different than what we saw for the minimax agent. The thing is that the harness around the agent matters a lot in the type of outputs that you're going to get. If In this case, if you provide the same prompt, it's going to use the same model to generate similar output. Now, in this case, we can select and then click on continue refinement. And I think we can probably uh tell it to fix this, but we can provide a subsequent prompt and it's going to continue modifying the images.

**10:26** · Now, if you look at the agent harnesses that we see around these models, these are plan, build, verify, and then iterate loops, which is very similar to this self-evolution concept as these labs are exploring now.

**10:45** · Uh in my opinion, M2.5 is a very capable model, uh especially the cost to performance ratio is pretty incredible.

**10:55** · All right. So, I'll highly recommend to test it out, and I'm especially excited about the open weight release. Also, where this self-evolution system is going to take us. Anyways, I hope you found this video useful. Thanks for watching, and as always, see you in the next one.