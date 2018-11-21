---
layout: post
excerpt_separator: <!--more-->
title: Go Lang and why You should care
tags: [go, golang, languages, technologies, adoption, serverless, efficient compute]
---

#  Go Lang and why You should care

Before drilling into [goLang](https://golang.org/) let's discuss why You should care about how technology changes and which change, when and how to adopt.

## Neverending progression

For those who've been in IT industry for a while it is quite apparent that there's no such things as staying still. As Heraclitus of Ephesus said: "Everything changes and nothing stands still" - or to rephrase it "There is nothing permanent except change".

<!--more-->

## Innovation

Innovation and adoption of innovative things should be bread and butter for technical people (and organisations providing digital solutions). Choosing what to adopt might not be easy though!

### Diffusion of innovations  

Diffusion of innovations is a theory that seeks to explain how, why, and at what rate new ideas and technology spread. Idea was popularized by Everett Rogers in his book "Diffusion of Innovations" (first published in 1962). Rogers proposes that four main elements influence the spread of a new idea: the innovation itself, communication channels, time and a social system. The innovation must be widely adopted in order to self-sustain (or it may fade away). Rogers categorized five types of innovation adopters:

1. **Innovators** - These are the people who want to be the first to try the innovation. They are venturesome and interested in new ideas. These people are very willing to take risks and are often the first to develop new ideas.
2. **Early Adopters** - These are the people who represent opinion leaders. They enjoy leadership roles, and embrace change opportunities. They are already aware of the need to change and so are very comfortable adopting new ideas.
3. **Early Majority** - These people are rarely leaders, but they do adopt new ideas before the average person. That said, they typically need to see evidence that the innovation works before they are willing to adopt it.
4. **Late Majority** - These people are skeptical of change, and will only adopt an innovation after it has been tried by the majority.
5. **Laggards** - These people are bound by tradition and very conservative. They are very skeptical of change and are the hardest group to bring on board.

In digital world if you (or the company) fall far to the right (please see diagram below), you are likely to lose competitive advantage.


![Diffusion of innovations](/assets/images/goLang2018/Diffusion_of_ideas.png)

*source: [https://en.wikipedia.org/wiki/Diffusion_of_innovations](https://en.wikipedia.org/wiki/Diffusion_of_innovations)*

### Future Predictability

Can we simply predict the future of technology? 

Back in 2016 Michael Mullany wrote a lessons learned [article](https://www.linkedin.com/pulse/8-lessons-from-20-years-hype-cycles-michael-mullany/) from 20 (well almost, 17) years of Hype Cycles published by Gartner every year.

The lessons were:
1. We're terrible at making predictions. Especially about the future.
2. An alarming number of technology trends are flashes in the pan.
3. Lots of technologies just die. Period.
4. The technical insight is often correct, but the implementation isn't there.
5. We've been working on a few core technical problems for decades.
6. Some technologies keep receding into the future.
7. Lots of technologies make progress when no-one is looking.
8. Many major technologies flew under the Hype Cycle radar.

I encourage a full read of the article. 

Can we simply predict the future of technology then? Not really.

## GO GoLang

Why should you care about goLang then?
1. Go is easy to learn.
2. Has mechanical sympathy build in.
3. Is one of the languages in AWS Serverless ecosystem.
4. It is getting more and more popularity and momentum.
5. Go ecosystem is starting to mature (but has not matured yet).

### GoLang community 

#### Values

GoLang values and code of conduct can be found [here](https://golang.org/conduct).

These are the values to which people in the Go community (“Gophers”) should aspire (all taken from the [https://golang.org/conduct](https://golang.org/conduct)).

- Be friendly and welcoming.
- Be patient.
    - Remember that people have varying communication styles and that not everyone is using their native language. (Meaning and tone can be lost in translation.).
- Be thoughtful.
    - Productive communication requires effort. Think about how your words will be interpreted.
    - Remember that sometimes it is best to refrain entirely from commenting.
- Be respectful.
    - In particular, respect differences of opinion.
- Be charitable.
    - Interpret the arguments of others in good faith, do not seek to disagree.
    - When we do disagree, try to understand why.
- Avoid destructive behavior:
    - Derailing: stay on topic; if you want to talk about something else, start a new conversation.
    - Unconstructive criticism: don't merely decry the current state of affairs; offer—or at least solicit—suggestions as to how things may be improved.
    - Snarking (pithy, unproductive, sniping comments).
    - Discussing potentially offensive or sensitive issues; this all too often leads to unnecessary conflict.
    - Microaggressions: brief and commonplace verbal, behavioral and environmental indignities that communicate hostile, derogatory or negative slights and insults to a person or group.

People are complicated. You should expect to be misunderstood and to misunderstand others; when this inevitably occurs, resist the urge to be defensive or assign blame. Try not to take offense where no offense was intended. Give people the benefit of the doubt. Even if the intent was to provoke, do not rise to it. It is the responsibility of all parties to de-escalate conflict when it arises.

#### Community

Go has a vibrant community of supporters. There are now over 20 [Go conferences](https://github.com/golang/go/wiki/Conferences) and over 300 [Go-related meetups](https://www.meetup.com/topics/golang/) spanning the globe. Some useful Go related links:
- [https://github.com/golang/go/wiki](https://github.com/golang/go/wiki)
- [https://blog.golang.org/](https://blog.golang.org/)
- [https://dave.cheney.net/resources-for-new-go-programmers](https://dave.cheney.net/resources-for-new-go-programmers)
- [https://forum.golangbridge.org/](https://forum.golangbridge.org/)
- [https://blog.newrelic.com/technology/golang-experts-follow-online/](https://blog.newrelic.com/technology/golang-experts-follow-online/)

### What other say about goLang?

It is in top 10 languages in Tiobe Index (November 2018):

|Nov 2018 |	Nov 2017 |	Change |	Programming Language |	Ratings	| Change|
|---|---|---|---|---|
|1	|1	||	Java|	16.746%|	+3.51%|
|2	|2	||	C|	14.396%|	+5.10%|
|3	|3	||	C++	|8.282%|	+2.94%|
|4	|4	||	Python|	7.683%|	+3.20%|
|5	|7	|▲	|Visual Basic .NET|	6.490%|	+3.58%|
|6	|5	|▼	|C#	|3.952%|	+0.94%|
|7	|6	|▼	|JavaScript|	2.655%|	-0.32%|
|8|	8	| |PHP	|2.376%	|+0.48%|
|9	|-	|▲	|SQL	|1.844% |	+1.84%|
|10|	14|	▲|	Go	| 1.495%  |	-0.07%|

![tiobe popularity](/assets/images/goLang2018/tiobe_popularity_chart.png)

It is in #5 Loved and #3 Wanted language according to [Stack Overflow survery](https://insights.stackoverflow.com/survey/2018/#most-loved-dreaded-and-wanted).

## Conclusion

Should you care about goLang then? As an architect I have to answer - "It depends". If you build mobile apps mainly, then probably no. If you want to build web services, lambdas, etc then  I believe the answer is yes. 

Should you jump in and adopt? For sure test out whether it fulfills your needs. Should you jump in adopt anything straight away? Most likely not.


