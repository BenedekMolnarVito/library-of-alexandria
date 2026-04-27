---
title: "Agents are autonomous except when they are not which is most of the time"
source: "https://generativeai.pub/agents-are-autonomous-except-when-they-are-not-which-is-most-of-the-time-a5de1408f417"
author:
  - "[[Marco van Hurne]]"
published: 2026-04-21
created: 2026-04-27
description: "Agents are autonomous except when they are not which is most of the time Good day to you my intelligent friend! I have been writing about running an agentification factory for the better part of two …"
tags:
  - "clippings"
---
![](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*f7X57rSHM9WaSn7wDx_o3w.png)

Good day to you my intelligent friend! I have been writing about running an agentification factory for the better part of two years now, and there’s this question that keeps arriving, in my inbox mostly and occasionally shouted across a conference floor by someone holding a lanyard and a vanilla sweet cream cold brew with extra vanilla sweet cream‡, and the question is this, “yeah fine and all, but how do you actually build one?”.

Not in theory, but how do you actually build one, in a real organization, with real data I mean, that is in the wrong format and with politics that nobody put in the project plan, and of course a CTO who just had forwarded a LinkedIn post about a new type of agent that can apparently do “everything”.

In my experience, the honest answer to that question has always been to invent it while you agentify. There is no shelf of proven blueprints. Those materials simply do not exist at the level of detail that we, the practitioners, actually need, so the only option has been to build, document, research and fail in instructive ways and then write it all down, and publish it before someone else claims they thought of it first. That is where the frameworks and papers I’m publishing come from and of course, that is where this article comes from.

One more thing before the lesson begins — a teacher will always be a teacher — the frontier AI labs are doing extraordinary work. We now have Xiaomi MiMo that has more than 1 trillion parameters with about 40B active parameters per token (it’s an MoE†), and since a few months there has been more talk about World Models than ever before, and all are models of staggering capability but the thing is that none of that is what enterprise actually needs right now. What enterprise needs, however, is a boring, trustworthy, *predictable* and reliable model that runs identically every single time and does not hallucinate a payment from five thousand euros to five hundred thousand euros, or gets creative with a compliance workflow, and hopefully doesn’t require three process operators on a Friday night to confirm that it behaved itself. The cool thing is that we’re designing this model at Eigenvector¥ and we’re targeting this specifically for what will be explained shortly as Zone III work. If you want to read more about this particular type of AI, read this piece “ [The boring AI that keeps planes in the sky | LinkedIn](https://www.linkedin.com/pulse/boring-ai-keeps-planes-sky-marco-van-hurne-flruf/) ”

The thing is that it is not glamorous AI¢ it certainly will not win a benchmark, but it will let a finance team run a payment process without the trauma that currently clings to most enterprise AI deployments like a fart.

And I say tho whom is looking into agentification of work, do not wait for it. The [35 percent agentification ceiling](https://www.linkedin.com/pulse/real-story-behind-enterprise-scale-process-marco-van-hurne-s2rqf/), which gets a proper explanation in this piece, is enough work to keep you busy for well over a year. So yea, the boring AI is coming, and in the meantime, there is an enormous amount to build.

Now, let’s get on with the blog!

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*8ZDPjBIO0i1Ni0lz)

‡ *Coffee for poofters*

† *Mixture of Experts. A federation of specialized models*

¥ *Ding Dong. Commercial interlude*

¢ *Ding Dong. Recruitment call. DM me if you want to build boring AI that keeps planes in the sky.*

## Congratulations on your AI Program, now let me explain why it will fail

Most of the enterprise AI programs that I’ve investigated for the paper that kickstarted my work in agentic process automation, they fail before they produce real value, and they fail in remarkably consistent ways. Now this information that would be useful before starting rather than after the budget review.

The [research](https://www.linkedin.com/pulse/real-story-behind-enterprise-scale-process-marco-van-hurne-s2rqf/) behind this is not anecdotal. It all started with an analysis of 177 documented enterprise agentic AI deployments across 20 sectors between 2022 and 2026. And in it, we identified ten primary *failure modes*.

The most frequent is data quality failure. That accounted for 31 percent of cases we reviewed. Nearly a third of deployments failed primarily because the data that is feeding the agent was either incomplete, inconsistent or incorrectly formatted, or simply wrong, and nobody had checked it before the darn thing went live. Then at second place there’s integration complexity that enters the hall of shame at 28 percent. Then governance overhead exceeding the return on investment at 25 percent and of course, there’s the dreaded hallucination in critical outputs that frocks up your program at 22 percent of cases.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*iz3eQoaJuVUVwRAT)

These four failure modes alone account for the majority of documented failures, and every single one of them is preventable if people had done a proper pre-deployment assessment. And the reason they keep happening is *impatience*. I see it in my programs as well. The exciting part of an AI program is of course the start, and the deployment of an agentified process, and the demos and certainly the moment when your fresh agent does something that makes a room go quiet. But the structural work that is required before any of that happens feels much like friction to the people involved, before the exciting part, so it gets either skimmed or skipped altogether.

There is also a more uncomfortable failure mode that our research documents, which is that many programs automate the wrong processes entirely. Not because they were poorly designed but because nobody assessed whether the process was suitable for automation in the first place. If you allow management pet projects in your factory, few of them will look sexy, but they will not deliver the promised results. Twelve percent of the cases we’ve documented are about cases where automation caused more harm than value. And they didn’t fail because of technology or governance failures, but they were simply lured into automating unsuitable (zone III) processes that got automated anyway because politics is not a framework and also that nobody had a better one.

The fix for all of this is a structured intake and triage process‡ that runs before any technology decision gets made, and a team with the discipline to actually use it.

Which brings the lesson to the question of what the factory actually is.

‡ *I created a site for that particular reason, it’s available at ai-automations dot my, but i’ve put it on hold for a while until the community token module is implemented, since you guys cost me an arm and a leg on Tokens every day.*

## We called it a Factory because Lab was already taken by something that also did not scale

An agentification factory is a structured, repeatable organizational capability and in it, you identify work that is worth automating, and you start by redesigning that work properly before even creating a single line of code. You automate what should be automated, and then you govern everything that runs and measure everything that matters, and when it all works without things exploding in your face, you then scales what proves its value. The word that matters most in that sentence, by the way, is *repeatable*. A single successful deployment is a project. A hundred deployments that are sharing tooling, governance, agentic patterns and laced with some institutional learning is called a *factory*. The difference is compounding. Each delivery gets cheaper, faster and better because the factory learns from every previous one.

Well, that is the idea at least.

And an innovation lab is not a factory. A center of excellence is not a factory either. And a collection of pilots that leadership tours on Fridays while some guy from IT explains what an agent is to a CFO who nods politely, well my friend, *that* is definitely not a factory. And it matters to make this distinction because organizations frequently tend to invest in the aesthetics of an AI program. Yeah, I’m talking about the cool team name, their Slack channel, the innovation space with the bean bags.

*Sigh.*

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*Eqb5hLAS_FT3ifZu)

But most of them aren’t investing in the operational infrastructure that makes any of it compound into value.

A factory runs on four streams.

And understanding how they relate to each other is the first structural lesson.

The process-improvement and -design work stream is the first and it is led by someone who can simultaneously manage process analysts, business architects, lean specialists and automation designers, and who works in close coordination with business process owners who are embedded in the operational units.

And no, simply appointing the most tech-savant worker as a process-owner is not going to lead to any tangible results. A process owner works on the business side of things and they are the people who are made responsible for the interface between the factory and the business. They own the candidate processes and they manage the local transformation. They also carry measurable KPIs for outcomes like the primary FTE release but also cycle time reduction, error rate improvement, compliance uplift and they’re the mechanism by which the transformation actually happens in the business.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*Fr7cDfFDgDCGqH1M)

The Automation Development† stream is the technical heart. This is where agents are built and you maintain your technical stack where the orchestration logic gets designed and tested and things like RPA, robotic process automation, handles the brittle deterministic interactions with legacy systems that agents cannot reliably manage. A small clarification on RPA because it gets confused with agents constantly, RPA is software that mimics human actions on a computer interface, and clicks buttons and copies fields and fills out forms and stuff. It is very precise and repeatable, but it does not think, only executes. On the opposite you have an agent that thinks and decides but often cannot reliably click the right button in a twenty-year-old SAP screen and in production, those two work together. The agent handles the judgment and orchestration layer. The RPA bot handles the pixel-perfect system interaction underneath it.

Then the Evidence workstream is about implementing the measurement and observability infrastructure that proves whether any of this is working and catches problems before they become expensive incidents. And last there’s your Change and HR stream to handle the human side of what happens when work gets automated, which is the stream that fails most consequentially when underfunded.

My personal mantra is to never let the change and workforce transition stream get defunded because behind every FTE release number on the dashboard sits a human being, and that is not a detail that belongs in an appendix, so when you’re undertaking such a feat, you need to think of a reskilling program. Luckily AI is not displacing jobs entirely (yet)‡, it is at the time of writing only capable of automating tasks up to max 70%, and that will buy people and organizations the time required to upskill or reskill people.

The core factory team itself should be kept deliberately small. This is what most programs get catastrophically wrong. The transformation must be owned and executed by the business, with the core team providing methodology, tooling, governance and pattern libraries. The moment the core team starts doing the work on behalf of the business, the factory becomes an expensive consultancy and the business leans back and becomes a spectator, and nothing survives when the program budget gets reviewed.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*S8FOacC1unKtEbW-)

† *Sometimes hyperautomation.*

‡ *Read “* [*Everyone’s job will be affected by AI and this is the uncomfortable evidence | LinkedIn*](https://www.linkedin.com/pulse/everyones-job-affected-ai-uncomfortable-evidence-marco-van-hurne-nkuhf/) ”

## The four zones nobody knows about

Here is where the ‘manual’ gets a tad technical, but that technical part matters a lot, because getting this wrong produces the 12 percent of deployments that cause more harm than value.

All work can be classified into four automation zones based on two dimensions:

- how suitable a process is for automation, measured by something called the Process Automation Suitability Score, and
- how complex the agent would need to be to execute it, measured by the Agent Complexity Level.

I’ve given this framework a lame name, ‘PASF’, the Process Automation Suitability Framework. I can’t help naming things that cannot be remembered, even by myself, I think it’s because I’m European.

> *Anyway, the research is solid and we validated it against those 177 deployments already mentioned, and it predicts deployment success with 74 percent accuracy.*

Something called a PASS score is calculated for each candidate to check it’s automation elligibility. This score itself is a weighted average of eight dimensions scored from zero to ten.

Here you go. All ten of ’em, structurability, rule-boundedness, data quality, reversibility, frequency and volume, exception density, stakeholder impact, and regulatory constraint and if you want to know what these mean, read “ [The real story behind enterprise scale process agentification | LinkedIn](https://www.linkedin.com/pulse/real-story-behind-enterprise-scale-process-marco-van-hurne-s2rqf/) ”.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*boGgUkQ_lsfuEnYz)

The last three are scored inversely by the way. This means that a high exception density causes a process to score low on this domain, high stakeholder impact also produces a low score, and high regulatory constraint produces a low score as well. A process scores well on the other hand, when it is highly structured, rule-based, data-quality rich, reversible, frequent, predictable, low-stakes and lightly regulated. Examples of these are processes like ‘invoice processing’ that scores an 8.6, and on the other hand, M&A negotiation scores a meager 2.1 as you may expect. These are not similar things and should not be approached similarly. That is also the reason why a shared service center is the ideal candidate for agentic automation because most processes are scoring high on the PASS chart.

Talking about which...

Zone I is the green zone. The Automate Now category. Well-executed Zone I deployments deliver 50 to 90 percent reduction in processing time and 30 to 70 percent reduction in cost per transaction. IT operations and customer service exhibit the highest mean PASS scores across sectors, at 8.4 and 8.1 respectively. Zone II requires piloting first, careful scoping, and mandatory human oversight at critical decision points. Zone III requires automation with significant caution, architectural governance controls, and ideally a boring predictable model, rather than a frontier model that might decide to be creative on a regulated output. Zone IV is the red zone. Do not automate there. The mean ROI for Zone IV deployments across the research dataset is negative 8 percent. The total cost of failure in Zone IV is approximately 15 to 20 times higher than in Zone I, and this is driven by reputational and regulatory costs that dwarf any efficiency gain. Trying to automate this zone is like playing Russian roulette. Five out of six times you’re ok.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*eNt_WfRZnGYRmLS7)

The agentification ceiling that we’re currently facing in agentification is approximately 35 percent of enterprise work. That is the realistic upper bound of what current AI can handle across Zone I and Zone II combined. Only 27 percent of the 177 deployments fell into the Automate Now category. Thirty-five percent sounds modest until you calculate the actual volume of work that it represents in a large organization. It is actually years of opportunity, and most organizations have not yet worked through year one of it properly.

> *Calculating the amount of work is now made possible through something we did with the PASF process automation framework and occupational classification frameworks called ONET and ESCO, which classify work by individual task rather than job title.*

This makes it possible to translate directly from a business process to the specific tasks within it and determine what percentage of a role is automatable. The instructive side effect of this analysis is that when actual task logs get mapped against job descriptions, a consistent discrepancy appears. People whose job descriptions describe Zone III cognitive work are frequently spending the majority of their working time on Zone I and Zone II tasks. The job description says say ‘strategic analyst’ or something along those lines, but then the task log we create as a result of our design work, says the job is more like a data formatter or email router and meeting scheduler. This has implications for workforce planning that extend well beyond the automation program itself.

That’s why we’re now also starting to use this data for strategic capability planning as well.

If you know what people are actually doing versus what their role says they should be doing, and you know what percentage of those actual tasks are automatable, you can start having a precise and honest conversation about what the organization needs from its workforce in three years rather than guessing. You can answer questions like which departments are carrying hidden Zone I capacity that automation will release and what roles are nominally senior but operationally routine, where the genuine Zone III capability actually lives, and whether it is being used or buried under administrative overhead.

Strategic capability planning built on task-level evidence is a fundamentally different exercise from the traditional HR competency framework discussion, and I find it increasingly more useful when the automation program starts moving fast, yet no HR officer has ever pro-actively reached out before.

## The frontier labs are building World Models and you still cannot find your process documentation

Before any agent touches any process, the process needs to exist in documented form. That’s an undisputed fact, but in most organizations it does not, or it exists at a level of detail that is entirely useless for automation purposes.

Process documentation has five levels, L1 through L5, and the level matters enormously for what you can do with it. If you never had to deal with process-work, here’s a quick course in Aris‡ lingo.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*nM8Tvd6U-3TM0KVr)

An L1 description is the name of the process, like ‘Accounts payable’, ‘Customer onboarding’, that sort of work. That is it. An L2 adds the major stages of such a process like say, receive invoice, validate, approve, pay. An L3 adds the steps within each stage, with decision points identified and an L4 adds the business rules, exception paths, system interactions and data field specifications for each step. Then you have an L5 that adds the task-level detail including triggers, data transformations, error conditions and technical interfaces. You’ll typically find instruction manuals reside at this level 5.

> *Well, when a process arrives at the development team and it’s at L2, than it gets sent back. Every time, because you cannot build an agent for a process you cannot describe, and you definitely cannot govern one.*

So we have this gate called the *intake process*, where documentation discipline gets enforced.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*KXW-Ga4OBIoAh32Z)

A candidate process enters the factory through an intake form that requires enough structural description to assess its basic characteristics. We ask questions to the process-owner before we can accept the idea, questions about volume, rule density, exception rate, data availability, reversibility of errors, regulatory exposure — that sort of thing. A process that cannot be described clearly enough to complete the intake form is a process that is not yet ready for automation, and that is useful information that saves months of wasted development time.

After the intake form comes this stage we call triage, and in this step we run the candidate through three gates before it reaches the development team. Gate one is the initial intake assessment. Gate two is the value, complexity and risk determination, where the PASS score gets calculated and the economics get quantified for the first time. The formula combines annual hours saved, hourly cost rates, implementation cost and governance overhead into a net value projection.

Processes that do not clear a minimum ROI threshold of approximately 200 percent in year one do not proceed. This is a rule of thumb, because there are always exceptions to the rule, especially when it comes to the compliance KPI.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*scEUa_BrC-fQkyrF)

Then gate three is the handover to development with a completed process blueprint, designed using PADE† thinking, which means the automation design has been derived from the process architecture rather than imposed on top of it. PASF by the way tells you whether to automate, and PADE tells you how to design it properly once you have decided to proceed. If you want to know more about how this works, download the paper from ResearchGate (in the comments).

The hyperautomation stack that the development team works with includes agents, RPA, workflow orchestration, API integration layers, monitoring and telemetry infrastructure, and test automation. They compose together into a working system, and the technology stack decision made early in the program determines what the triage formula can cost-estimate for new candidates, which is why that decision needs to happen in the first thirty days rather than the first three hundred.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*YjvaNvcsHmryG7bh)

‡ *Aris is the name of a process modeling tool used in lots of enterprises.*

† *Process Automation Design (... Engine. Ok, lame, I know — for lack of a better acronym).*

## Yes you also need governance, no you cannot skip that part

Governance is the word that separates AI programs that survive from AI programs that become case studies in what not to do, and it is the word that gets treated most consistently as something to add later when the exciting part is finished.

> *At Agent Complexity Level 1, the lowest complexity tier, governance overhead consumes approximately 8 percent of total project cost. By Agent Complexity Level 5, that number is 72 percent. Seventy-two percent of the project budget goes to making the system safe, auditable and controllable. At that level the efficiency gains from automation have been largely consumed by the cost of governing it, which is the primary economic reason that Zone IV work should not be automated and why the governance overhead problem is central to understanding the agentification ceiling.*

What governance actually means in practice is building trust through activities such as explainability, the ability to show why an agent made a specific decision in a specific case, in a form that a regulator or auditor can read and verify. Trust also means traceability or the ability to follow every action the agent took through a complete and unbroken audit trail from the triggering input to the final output. It also means observability. This is the real-time monitoring of agent behavior to detect anomalies before they propagate through downstream processes and become expensive. It also means introducing kill switches, and I mean actual tested working kill switches that halt a process instantly. Tested ones preferably.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*N8qf9vkWMXXsOGDN)

The process operator role is the human layer that makes all of this functional.

I graduated a long long time agao as a chemical engineer, and in chemical manufacturing, a process operator monitors a continuous industrial process through instrumentation panels. They interpret signals, intervene when parameters drift outside acceptable ranges and escalate things when something cannot be solved.

That same logic applies directly to agentic factories.

Here, the process operator watches the control tower dashboards and looks at the telemetry coming from the orchestration and RPA layers where he tries to catch the anomalies that the monitoring system flags but cannot resolve, and he has the authority and the training to stop a process when necessary.

And now you know why this is not a junior role, and why it pays well, because it requires understanding of both the business process and the automation architecture well enough to distinguish a genuine anomaly from normal operational variation.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*DaCrQeBlZEIzFmPj)

The evidence factory† is the infrastructure that *agentic process operators* work within, and it has three distinct purposes. It is where operational monitoring and escalation happens including troubleshooting and root cause analysis. It is also producing the data which is most important for your program survival, which is measurement of Net Program Value.

The NPV formula combines realized efficiency gains against governance costs, infrastructure costs, change management investment and training cost and it ends up becoming a single number that tells your boss if your factory is creating value or simply creating activity. This number should be in your face and updated weekly and should be visible to anyone in the team and to the people who own a budget line in the program.

If it is not, the evidence factory has not been built and the program is running on faith.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*4EwfJU5yyuj7vnvf)

And tokenomics‡ is one of those disciplines that are being managed at the evidence factory.

Tokenomics is about managing the economics of running AI at scale, and it deserves specific attention because it catches AI programs by surprise at volume.

What I lovingly call ‘ *Pennywise Tokenomics* ’ addresses the per-transaction inference cost — what does it cost in compute to run this agent on this process instance — and does that cost remain acceptable at ten times the current volume.

A concrete example will explain what I mean with this. Say, you have an agent that processes an invoice costs 0.003 euros per run. This looks mighty fine on the outside, but when you multiply that by 400,000 invoices a year across a large finance operation and you are suddenly looking at 1,200 euros a year in inference cost for one process alone, before infrastructure, before monitoring, before the three other agents touching the same workflow.

Ok, that can still be manageable, but now add the agents for purchase orders, vendor onboarding, payment matching and exception handling, and the number climb up rapidly.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*PHUPDCnZMFECNsa9)

Then there’s this metric that I call ‘ *Poundwise Patternomics* ’ that tries to optimize the structural cost patterns that emerge across a portfolio of agents that are running at the same time.

You can have an individual unit costs look fine but aggregate compute consumption can make your whole program uneconomic. The pattern that kills programs is not the one expensive agent, though scaling it makes it very painful to the wallet. No, it is actually forty moderately priced agents all calling the same large language model simultaneously at peak processing hours, and none of them are batched or cached, and all of them are running full inference on inputs that are 80 percent identical to something already processed ten minutes ago.

> *In other words, you also have to optimize your own agentic patterns in the workflows they support, because the costs will go up dramatically at scale.*

A brilliantly designed agent with unmanaged tokenomics can produce negative ROI at scale even when every individual deployment dashboard looks healthy. This is the compute bill that arrives in month eight and makes a CFO ask questions nobody prepared answers for.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*QITBE_2zpkozGeWU)

† *If you want to know more about how to organize the intake process, and setting up a value office, read the paper in the comments.*

‡ *If you want to read more about Tokenomics at scale, read this blog — and the paper in the comments — “* [*I spent a year burning money on AI and finally decided to do something about it | LinkedIn*](https://www.linkedin.com/pulse/i-spent-year-burning-money-ai-finally-decided-do-marco-van-hurne-gwtcf/?trackingId=h9EuyTe%2BRC68329C45Ym%2Bw%3D%3D) *”*

## Your AI pilot was a great success! (but will now quietly retire)

JPMorgan Chase has publicly stated a vision of AI agents powering their every internal process. Salesforce built Agentforce. AWS has Bedrock Agents.

The ambition of most companies — especially in the US, but less in Europe — is real and the marketing surrounding it is even more extraordinary, but the gap between the marketing and the current operational reality of most enterprises is where a significant portion of the tech-consulting industry currently lives, and it is comfortable accommodation for those companies.

From the assessment we ran, we concluded that most enterprises have deployed between one and five agentic AI use cases in production, and they managing them with significant manual oversight. These companies are also nowhere near any version of a factory model. The realistic near-term goal for most organizations is not a factory but an automation portfolio of five to twenty Zone I deployments, each with well-defined scope, measurable success criteria and appropriate governance. And they are generating consistent and provable ROI, yet not enough to cover the initial investments. So if you are considering a factory approach, you’re looking at a two to five year aspiration.

The pilot that succeeds and then retires is the most common trajectory we see in enterprise AI.

The pilot process works perfect in a controlled environment with a dedicated team and careful data preparation. Then the dedicated team moves on, the data preparation step is handled with less care and the monitoring gets deprioritized because of budget constraints, and then the agent starts making errors that nobody catches until the errors become visible in downstream outputs. The reason this happens is of course organizational. The business never truly owned the deployment, and a program team built it, proved it, handed it over, and discovered that the business receiving it had no operational capability to maintain it.

That is why the business itself — the departments you’re trying to automate need to take ownership.

The business process owner who carries the KPIs for cycle time reduction and error rate improvement has a direct personal interest in the agent working correctly, which is a far more reliable governance mechanism than a quarterly review by a program team that has moved on to the next deployment.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*O69W1CBLzZaiN8cV)

## And then you automated the wrong thing beautifully and on budget

Change management is the stream that fails most often, and the workforce transition question is the one that organizations consistently treat as a communications problem rather than an operational one. Yes, there’s a difference.

You simply cannot treat people like legacy systems. They do not get deprecated on a schedule and replaced with a new version that runs faster.

When Zone I work gets automated to a high degree, and the people who were doing that work are still employed, the question of what they do next is not going to resolve itself. It requires deliberate investment in reskilling, and role redesign and also in honest conversations about where work is going and what the organization needs from human beings once the routine processing layer is running autonomously.

> *Fatih Boyla, a sharp thinker and someone worth listening to on this subject, put it well when he said “As the tasks of a job get automated, the focus needs to shift toward adding value to the purpose of that job”.*

What he means is that a job can be seen as a list of tasks you finish before end of day. If that is your view, you will become obsolete in the age of AI. But you need to change your view of a job through the lens of its purpose, something the organization wants to happen in the world. Say you are an accounts payable clerk processing invoices, and processing them is now your task, which is one of the easiest to automate, but the purpose of that role is to ensure the organization meets its financial obligations accurately, on time, and in compliance with its agreements. The tasks, matching invoices, chasing approvals, entering data, are just the current mechanical expression of that purpose.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*FMQXeM19rxbcG6-a)

When the tasks get automated, the purpose does not disappear.

The organization still needs someone who understands vendor relationships or catches the structurally odd invoice that the agent flagged but cannot interpret, who notices that a supplier has secretively changed their payment terms or who can have a conversation with a CFO about cash flow timing. None of that is a task in the traditional sense, but all of it is purpose work.

The reason this matters for workforce transition is that most people identify with their tasks rather than their purpose, because tasks are visible and they’re familiar. Telling someone their tasks are being automated feels like telling them their job is disappearing, even when the purpose of that job is expanding in importance. The retraining conversation therefore needs to start with what the role actually exists to achieve and *not* with what the automation will replace, and then work forward from there toward the capabilities that serve that purpose in a world where the routine processing layer runs itself.

The task-level analysis we did, connecting PASF to ONET and ESCO frameworks makes this conversation even more precise than it has historically been. When it becomes possible to say, specifically, that 60 percent of what this team currently does falls into Zone I and Zone II, and here are the Zone III capabilities that the role description says they should have but that the task logs show they are not currently exercising, the workforce transition conversation changes from a vague anxiety about jobs to a specific design problem about capability development. That is a solvable problem. The vague anxiety version is not.

## Congratulations, you read to the end, now go build something

Building an agentification factory is *not* really an AI project. You are actually building an organizational capability problem that happens to involve AI, which is a sentence that nobody who has spent three months debugging an orchestration layer will say with a straight face, but which is nonetheless true at the program level. This means ownership needs to be with the business and not IT because the technology is the tractable part, but the data quality, the governance discipline, the business ownership, the workforce transition, the institutional patience to build a portfolio before claiming a factory, well, those are the hard parts, and no IT organization can solve that for you.

![](https://miro.medium.com/v2/resize:fit:1400/format:webp/0*KcvGmeIep995u30F)

*So, build your factory.*

The research exists. The frameworks exist. The patterns, failure modes, intake tools, triage formulas, governance requirements and NPV calculations, they all exist. But what remains is the work, which turns out to be the part no handbook can do, including handbooks that explain themselves with the same paragraph twenty-four times.

Go boldly my friend. Take notes. Build the boring AI, and remember, *the factory does not care how good the slide deck was.*

*Signing off,*

Marco

> Eigenvector builds Agentification factories at scale, for production environments that actually have to pay-off, and Eigenvector Research occasionally publishes papers about why this is harder than the demos suggest.

*👉 Think a friend would enjoy this too? Share the newsletter and let them join the conversation.* LinkedIn, Google and the AI engines appreciates your likes by making my articles available to more readers.[https://medium.com/@yanli.liu](https://medium.com/@yanli.liu)