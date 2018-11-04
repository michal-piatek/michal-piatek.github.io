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

In this blog I will summarise the learning and will add opinions of my own. Slides and keynotes videos can be found [here](https://conferences.oreilly.com/software-architecture/sa-eu/public/schedule/proceedings).

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
|10-page literal Pascal program, <br/> including innovative new data structures|tr -cs A-Za-z '\n' \|<br/>tr A-Z a-z \|<br>sort \|<br>uniq -c \|<br>sort -r -n \|<br>sed ${1}q|

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

### Introducing Serverless to your organization

Mike Roberts defined Serverless as:

> Serverless = BaaS + FaaS

And three interesting attributes serverless approach has:
- No concern of managing server machine or processes
- Automatic and invisible auto-scaling (based on usage)
- Costs based on precise usage

Mike stated (quite rightly so) that serverless approch let's you trial things really quickly and cheaply - you can be live within hours.

Migration to serverless (from current architectures) would be an iterative approach. There will be **competing** three goals that will be taken into consideration while talking about serverless adoption:

![Goals](/assets/images/SAC2018/serverless_introduction_to_organisations_goals.png)

Mike defined four levels of serverless usage within a project:

|Level|Description|
|:---:|:---:|
|Level 1|Serverless Operations|
|Level 2|Offline Tasks|
|Level 3|Serverless Activities|
|Level 4|Serverless Ecosystem|

**Level 1** - e.g. Environment reporting, ChatOps / SlackBots, Deployment automation, Monitoring & Log processing

This level can be categorised as:

![Level 1 goals chart](/assets/images/SAC2018/serverless_introduction_to_organisations_level1.png)

**Level 2** - A cron / jobs box replacement. This level:
- Introduces FaaS techniques for application development and deployment, while keeping out of real-time logic flow
- Easy to swap in and out with traditional implementations
- BUT not useful for learning about high throughput scenarios
- Serverless is not great for long running batch jobs

This level can be categorised as:

![Level 2 goals chart](/assets/images/SAC2018/serverless_introduction_to_organisations_level2.png)

**Level 3** - real time components of a bigger whole, e.g. message processing lambdas, external service integrations, isolated microservices (without downstream dependencies). This level:
- Bring Serverless advantages to real-time scenarios
- Learning how to use Serverless for real-time events
- Serverless technologies contained to specific areas
- Not completely safe from scale (e.g. if downstream is not as scalable)
- Hard to understand full benefits of holistic Serverless ecosystem

This level can be categorised as:
![Level 3 goals chart](/assets/images/SAC2018/serverless_introduction_to_organisations_level3.png)

**Level 4** This level:
- Brings use of Serverless right up to UX boundary
- Full immersion learning
- Opportunities to use higher level types of learning
- Understanding what Serverless architecture looks like
- If things go wrong could easily impact other areas of organization, even **non** Serverless ones

This level can be categorised as:
![Level 4 goals chart](/assets/images/SAC2018/serverless_introduction_to_organisations_level4.png)

#### Serverless usage

- Website and application
- Serverless Data Pipeliness
- Collections of Services   

### Implementing microservices as a serverless application

Nikhil Barthwal gave a comparison between microservices build on top on IaaS (mainly) and Serverless architecture.
On a high level with serverless:
- you have less infrastructure to care about, but you have less control
- real-life examples tend to by a classical microservice and serverless

When we think about compute (FaaS) in serverless:
- it is asynchronous (event driven)
- has cold start problems
- we get a vendor lock in (unless we abstract it out and get lowest common denominator from various cloud providers)
- security is a different beast (but containers are short lived, which helps with making it more secure)
- distributed transactions - use Saga pattern
- resiliency - use circuit breakers, connection pools and BaaS
- functionality should be fine grained
    - Functions have resource limits
    - Functionality should be as small as possible
    - Continiuous refactoring is needed
- Function groups should not share Data stores - each fucntion group should have a single BaaS backing it up
- When doing schema changes a deployment of an entire function group may be needed

### Applying the principles of chaos to serverless
Yan Cui started of with a defition of chaos engineering (from [http://principlesofchaos.org/](http://principlesofchaos.org/)):

> Chaos Engineering is the discipline of experimenting on a distributed system in order to build confidence in the system’s capability to withstand turbulent conditions in production.

and did a parallel to vaccination - *Chaos Engineering is the vaccine to frailties in modern software*. In that context Chaos Engineering:
- Uses controlled experiments to inject failures into our system
- Helps us learn about our system's behaviour and uncover unknown failure modes, before they manifest like wildfire in production
- Lets us build confidence in systems stability to withstand turbulent conditions

Chaos engineering is not about breaking things it is about learning about the system and building confidence.

There are four steps to run a chaos experiment:
1. Define "steady state" - what does normal, working condition look like (we don't want to run chaos experiment on system that's not healthy)
2. Hypothesise steady state will continue in both control group & the experiment group - you should have a reasonable degree of confidence the system would handle the failure before you proceed with the experiment
3. Inject realistic failures - e.g. server crashes, network error, HD malfunction, etc
4. Disprove hypothesis - i.e. look for difference in steady state

Chaos experiment in practice:
- Explore unknown unknows away from production
- Experiments that graduate to production should be carefully considered and planned
- You should have reasonable confidence in the system before running experiments in production
- Treat production with care it deserves
- The goal is not to break things
- If you know the system would break and you did it anyway, then it's not chaos experiment! - it's called being irresponsible
- Look for evidence that steady state was impacted by the injected failure
- Address weaknesses before failures happen for real
- Experiments need to be controlled

Containment:
- Ensure everyone knows what you are doing
- Don't surprise your teammates
- Run experiments during office hours
- Avoid important dates (e.g. new season of "Game of Thrones" on Netflix)
- Make the smallest change necessary to prove or displrove hypothesis
- Have a rollback plan
- Stop the experiment right away if things start to go wrong
- Don't start in production
- Can learn a lot by running experiment in staging

#### New challenges with Serverless
- There are no servers that you can access and kill. 
- There are more inherent chaos and complexity in a serverless architecture.
- Smaller unit of deployment, but a lot more of them.
- Every function needs to be correctly configured and secured.
- A lot of managed, intermediate services, each with its own set of failure modes.
- Unknown failure modes in the infrastructure we don't control.
- Often there's little we can do when an outage occurs in the platform.

#### Common weaknesses
- Improperly tuned timeouts (a caller times out before called service responded)
- Missing error handling (generic error propagation with HTTP 500 as an example)
- Missing fallback (how will I react when dynamoDB I am calling is having an outage)
- Missing regional failover

#### Latency injection with serverless
**Step 1.** Steady state
- what metrics do you use
    - p95
    - p99
    - error count
    - backlog size
    - yield (percentage of request completed)
    - harvest (completeness of the returned response)

**Step 2.** Hypothesise steady state will continue in both control group & the experiment group

Serverless considerations:
- API Gateway integration timeout is 29 seconds
- Cold start effect - how does it affect your strategy for handling slow responses

**Request timeouts**

Strategy should:
1. Give requests the best chance to succeed.
2. Do not allow slow responses to timeout the caller function

Finding the right timeout value is tricky:
- **too short** - requests not given the best chance to succeed
- **too long** - risk timing out the calling function
- It is even more complicated when you have multiple integration points 

Approaches:
1. Split invocation time equally (e.g. 3 requests, 6s timeout -> 2s timeout per request)

![Equal timeouts distribution](/assets/images/SAC2018/chaos_theory_timeouts_equal_distribution.png)

{:start="2"}
2. Every request is given nearly all the invocation time (e.g. 3 requests, 6s timeout -> 5s timeout per request)

![Almost all timeout](/assets/images/SAC2018/chaos_theory_timeouts_almost_whole_invocation_time.png)

{:start="3"}
3. Set timeouts dynamically based on invocation time left

In AWS Lambda

> **Context Object Methods**
>
> The context object provides the following methods.
> 
>**context.getRemainingTimeInMillis()**
>
>Returns the approximate remaining execution time (before timeout occurs) of the Lambda function that is currently executing. The timeout is one of the Lambda function configuration. When the timeout reaches, AWS Lambda terminates your Lambda function.
>
>You can use this method to check the remaining time during your function execution and take appropriate corrective action at run time.
>
>The general syntax is:
>
>```javascript
>context.getRemainingTimeInMillis();
>```

![Dynamic allocation - success](/assets/images/SAC2018/chaos_theory_timeouts_dynamic_success.png)
![Dynamic allocation - failure](/assets/images/SAC2018/chaos_theory_timeouts_dynamic_failure.png)

Recovery steps:
- Log the timeout with as much context as possible
  - The API, timeout value, correlation IDs, requests object, etc
  - Record custom metrics
- Use fallbacks
- Be mindful when you sacrifice precision for availability (e.g. your account balance) - User Experience is the king.

**Step 3.** Inject realistic failure
Where to inject latency?

![Where to inject - sample](/assets/images/SAC2018/chaos_theory_timeouts_latency1.png)

##### **Hypothesis** Function has appropriate timeout on its HTTP communications and can degrade gracefully when these requests are time out.
![Latency injection](/assets/images/SAC2018/chaos_theory_timeouts_latency2.png)

Should be applied to 3rd party services too (DynamoDB, Twilio, Auth0, ...) 
![Latency injection - 3rd part](/assets/images/SAC2018/chaos_theory_timeouts_latency3.png)

Be mindful of the blast radius of the experiment - goal is not to break things!

![Latency injection - blast radius](/assets/images/SAC2018/chaos_theory_timeouts_latency4.png)

##### **Hypothesis** All function have appropriate timeout on their HTTP  communication to this internal API, and can degrade gracefully when requests are timed out.

![Latency injection - big imact](/assets/images/SAC2018/chaos_theory_timeouts_latency5.png)
![Latency injection - big blast radius](/assets/images/SAC2018/chaos_theory_timeouts_latency7.png)

*Use failure injection to programme your colleagues into thinking about failures modes early.*

Make X% of all requests slow in the dev environment.

![Latency injection - big blast radius](/assets/images/SAC2018/chaos_theory_timeouts_latency6.png)

##### **Hypothesis** The client app has appropriate timeout on their HTTP communication with the server, and can degrade gracefully when requests are time out.
![Latency injection - client](/assets/images/SAC2018/chaos_theory_timeouts_latency8.png)
![Latency injection - client imact](/assets/images/SAC2018/chaos_theory_timeouts_latency9.png)

**Step 4.** Disprove hypothesis
How to inject latency?
- Static weavers (.g. PostSharp, AspectJ)
- Dynamic Proxies
- [https://theburningmonk.com/2015/04/design-for-latency-issues/](https://theburningmonk.com/2015/04/design-for-latency-issues/)
- Manually crafted wrapper libraries
- factory wrapper functions (think bluebird's *promisifyAll* function)

Code samples from [https://github.com/theburningmonk/lambda-latency-injection-demo](https://github.com/theburningmonk/lambda-latency-injection-demo)

```javascript
'use strict';

const co      = require('co');
const Promise = require('bluebird');

let injectLatency = co.wrap(function* (config, segment) {  
  if (config.isEnabled === true && Math.random() < config.probability) {
    let delayRange = config.maxDelay - config.minDelay;
    let delay = Math.floor(config.minDelay + Math.random() * delayRange);

    console.log(`injecting [${delay}ms] latency to HTTP request...`);
    
    yield Promise.delay(delay); // <- important bit
  }
});
```

```javascript
let Req = function* (options) {
  let request = getRequest(options);
  let fullResponse = options.resolveWithFullResponse === true;

  let latencyInjectionConfig = options.latencyInjectionConfig;
  yield injectLatency(latencyInjectionConfig, subsegment); // <- important bit

  try {
    let resp = yield exec(request);
    return fullResponse ? resp : resp.body;
  } catch (e) {
    if (e.response && e.response.error) {
      throw e.response.error;
    }
    
    throw e;
  }
};
```

#### Error injection with serverless
Approach is similar to latency injection. Most common errors are:
- HTTP 5xx (can be simulated by injecting 5xx responses in http client)
- DynamoDB provisioned throughput exceeded (can be simulated by injecting the exception in AWSSDK wrapper)
- Throthled Lambda invocations (can be simulated by setting reserved concurrency limit)

#### Recap
- failures are **INEVITABLE**
- the only way to truly know your system’s resilience against failures is to test it through **CONTROLLED** experiments
- the goal of chaos engineering is **NOT** to actually break production
- **CONTAINMENT** should be front and centre of your thinking
- Follow the 4-stepped chaos engineering experiment blueprint
- there are more inherent chaos and complexity in a serverless application
- even without servers, you can still inject **CONTROLLED** failures at the application level


Thanks for reading - hopefully you enjoyed it!
