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

## Why architects fail



