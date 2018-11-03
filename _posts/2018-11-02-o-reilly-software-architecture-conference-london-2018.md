---
layout: default
excerpt_separator: <!--more-->
title: O'Reilly Software Architecture Conference - London 2018
tags: [k8s, architecture, microservices, event-driven, serverless, lambda]
---

# O'Reilly Software Architecture Conference - London 2018

Software architecture is an interesting and broad subject. It is a backbone of the (succesful) software delivery and not only the Architects thing. On the talks I had the pleasure to attend few common themes surfaced:

- Technology: Containers (k8s), Message Brokers (e.g. Kafka) and Serverless (FaaS and BaaS) are the main focus in the industry
- We all make mistakes - key thing is recovery (evolutionary architecture, design for failure, observability, chaos engineering)
- Microservices as an approach - especially in event-driven approach (Message Broakers, Queues, NoSql Stores)
- CQRS as an approach (AxonIQ as a sample framework)
- Business is the key, technology is just an enabler - embracing the MVP and time-to-market thinking is important

<!--more-->

In this blog I will summarise the learning and will add opinions of my own at the end. Slides and keynotes videos can be found [here](https://conferences.oreilly.com/software-architecture/sa-eu/public/schedule/proceedings).

## Why software architects fail (and what to do about it)

Stefan Tilkov described 10 diseases of a software architect.

1. **Over-generalization drive**

Symptom: *Seeing commonalities in everything and turning them into generic solutions*

Stefan told a funny anecdote about stages of architect career:

(1) **The Enthusiastic Developer** - "This stuff is cool - let's build programs! For real people!"

(2) **The Disilusioned Developer** - "Oh. Real people have boring problems." 

(3) **The Enthusiastic Architect** - "Generic solutions! Cool!" 

(4). **The Disillusioned Architect**  - KISS, YAGNI, Lean, Minimal Viable Product, Story focus

Followed by quote from [Joel Spolsky](https://www.joelonsoftware.com/2001/04/21/dont-let-architecture-astronauts-scare-you/):

> When you go too far up, abstraction-wise, you run out of oxygen. Sometimes smart thinkers just don’t know when to stop, and they create these absurd, all-encompassing, high-level pictures of the universe that are all good and fine, but don’t actually mean anything at all.
>
> These are the people I call Architecture Astronauts.

(5) **The "Wise" Architect**

Quesion: *\** (any question)

Answer: *it depends*

{:start="2"}
2. **Domain Allergy**

Symptom: *Treating the domain as a negligible nuisance* 

![Domain allergy, generics](/assets/images/SAC2018/domain_allergy_generic.png)

{:start="3"}
3. **Obsessive Specialization Disorder**

Symptom: *Believing evry problem to be unique, even if it's been solved 1,000 times*

An anecdote to illustrate the point:

**Task**: Read a file of text, determinethe *n* most frequently used words, and point out a sorted list of those words along with their frequencies

| **Donald Knuth** | **Doug McIlroy** |
|:---|:---|
|10-page literal Pascal program, <br/> including innovative new data structures|tr -cs A-Za-z '\n' \|<br/> tr A-Z a-z \|<br>sort \|<br> uniq -c \| sort -r -n \| sed ${1}q|

{:start="4"}
4. **Unhealthy Complexity Attraction**

Symptom: *Being so smart you can't be bothered  by simple approaches*

{:start="5"}
5. **Analysis Paralysis**

Symptom: *Taking longer to evaluate than to actually do it*
![Vendor selection](/assets/images/SAC2018/vendor_selection.png)

{:start="6"}
6. **Innovation Addiction**

Symptom: *Things become progressively less fun the closer you get to production*

Symptom: *Using fashionable technology because it's popular (a.k.a. conference driven architecture)*

Finished with a quote from [Dan McKinley](http://mcfunley.com/choose-boring-technology)

> "Mindful choice of technology gives engineering minds real freedom: the freedom to contemplate bigger questions. Technology for its own sake is snake oil."

and described idea of innovation tokens. Innovation tokens are limited in a given time period (e.g. 3 innovation token in a year time). You can spend innovation token to change your DB engin as an example. You cannot have all the innovations you want so you have to spend the innovation tokens wisely.

{:start="7"}
7. **Severe Tunneling Fixation**

Symptom: *Enforcing an architectural approach that clashes with the framework, libraries or tools you use* 

{:start="8"}
8. **Asset Addiction**

Symptom: *Becoming so attached to a particular tool/library/framework it becomes a fit for every problem*

{:start="9"}
9. **Exaggerated Risk Aversion**

Symptom: *Sticking with horrible, horrible, HORRIBLE tools because they're there*

Symptom: *Confusing "easy" with simple, creating additional complexity*

Distinction of the following attributes of architectural decisions can by found on Rich Hickey talk ["Simple Made Easy"](https://www.infoq.com/presentations/Simple-Made-Easy). 

|simple|easy|
|hard|complex|

On a high level simple is the opposite of hard and easy is the opposite of complex.

{:start="10"}
10. **Impact Dissonance**

Symptom: *Becoming too detached from the actual system that is being delivered* 

As a result architecture becomes a thing of its own and in mind of few becomes more important than the appliocation itself, which is clearly wrong.

Symptom: *Believing everything has to be approved by you to ensure it meets the architecture standards*

Beware the megalomania syndrome!

#### The architect

**What architects want to do?**
- Shape strategy (30%)
- Make important decisions (30%)
- Explore technologies (20%)
- Mentor developers (20%)

**What others think the architects do**
- Define annoying rules (40%)
- Slow down development (20%)
- Pick the wrong tools (20%)
- Refuse to learn from devs (20%)

**What developers *actually* do**
- Try to be involved (35%)
- Act as sales people (30%)
- Defend architecture (30%)
- Do technical stuff (5%)


#### How to cure the above diseases?

Stefan defined a very broad (and not to be taken literally) success formula.

**An Architect's Success Formula**
|Dogma and rules|10%|
|Experience|20%|
|Pragmatic|20%|
|Flexibility|10%|
|Minimalism|10%|
|Trends and Future needs|10%|
|Experiment & PoCs|10%|
|Hands-on participation|10%|
|Vendor advice|0%|

## Microservices

### Anti-patterns

**Chris Richardson** described anti-patterns (mainly in the context of migrating from monolith to microservices, but I believe most of them are more generic than this context):

1. **Magic pixie dust** - believing a sprinkle of microservices will solve the development problems. The main idea around microservices is lousely coupled architecture with lousely coupled teams. It enables testability and deployability that enables CD / DevOps. The actual problems organisation faces are:

  - deployment pipeline is slow, silo'd. Manual deployment and testing
  - Applications are big balls of mud
  - Stinky code
  - Duplicate codebase
  - ...

  If organisations migrate to microservices with the above problems it is likely it will be a disappointment as the problems will remain (or get even worse!).

  Problems can be fixes as following:
  - deployment pipeline is slow, silo'ed. Manual deployment and testing => DevOps, small autonomous teams, automated deployment pipeline, etc
  - Applications are big balls of mud => rearchtect, maybe to microservices
  - Stinky code => learn how to write clean code and enforce code quality
  - Duplicate codebase => combine and design extension points

{:start="2"}
2. **Microservices as a goal** - leadership announces a microservices transformation initiative. Bonus ∝ #microservices.

  High-level support is essential BUT:
  - Ignores other obstacles to rapid, frequent and reliable software delivery
    - Processes - waterfall process, manual testing, manual deployment
    - Organisation - silo'd teams
    - Software - big ball of mud, stinky code, ...
  - Imposes an architecture on teams even when it does not make sense
  - Teams might not understand the goal

  Better goal: rapid, frequent and reliable software delivery
  - Key metrics to improve:
    - Lead time - time from commit to deploy
    - Deployment frequency - number of deploys per day
    - Failure rate - how often deploy fails
    - Recovery time - time to recover from outage
  - Application teams decide how to improve these metrics

{:start="3"}
3. **Scattershot adoption** - multiple teams independently adopting microserviceswith no coordination.
  Problems:
  - Duplication of effort, e.g. building infrastructure for deployment pipelines and runtime environments 
  - Development teams might not have the skills to build infrastructure

  ![Microservices adoption strategy](/assets/images/SAC2018/microservices_adoption_strategy.png)

{:start="4"}
4. **Trying to fly before you can walk** - an organisation attempts microservices while lacking key skills, e.g. clean code, object-oriented design, test automation, ...  
  Solution:
  - Assess skills level of each developer and team
  - Establis training, etc. program to improve skills
  - Re-evaluate whether you still need the microservice architecture

  ![Learn walk to fly](/assets/images/SAC2018/walk_to_fly.png)

{:start="5"}
5. **Focusing on technology** - vendors telling you to buy their cool stuff => Organisation focus on infrastructore, not on application architecture - what's important here is able to deploy to production, not building a thing that will tackle all possible scenarios without ever delivering it.
  - Infrastructure = undifferential heavy lifting
  - Big upfront investment = Decision made without experience (e.g. paying a lot of money to certain vendors)

  **Focus** on the essense of microservices: service decomposition and definition. 

  Build **just** enough infrastructure.

{:start="6"}
6. **The more the merrier** - planning to have a large number of services:
  - Risk of unnecessary complexity
  - Risk that changes impact numerous services

  A proposed approach is to start with small (2 pizza teams) per service and split the team when service needs splitting to more services.

  ![Service per team](/assets/images/SAC2018/service_per_team.png)

{:start="7"}
7. **Red flag law** - adopting microservices without changing process, poslicies and organization:
  - Silo'd teams
  - Manual testing
  - Monthly deploys at midnight
  - ...

  The following approach should be taken to mitigate:
  ![Improve processes, organization and architecture](/assets/images/SAC2018/improve_processes_and_organization.png)

  ![Introduce microservices incrementally](/assets/images/SAC2018/microservices_incrementally.png)

More on the microservices can be found in newly published book by Chris "Microservice Patterns".

## Serverless

## Event-driven architecture




