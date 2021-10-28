---
layout: post
title:  "Monoliths, Microservices and Culture"
date:   2018-05-03 19:00 +0300
image: "/images/monolith/iceberg.png"
description: "do you think that Microservices are only related to technology?"
tags:   [Digital Transformation, Microservices]
---

Microservices are in the air, in everywhere but when someone talk about Microservices, the most of times, they are talking about "technical" aspects:

- Take your code and refactor it in independent services.
- Introduce new tools and concepts like Netflix stack
- Move to a PaaS, Docker, Kubernetes,...,etc
- Install an Enterprise Event Bus like Kafka or RabbitMQ
- ...


This could be great but do you think that Microservices are only related to technology?


## A short story

Once upon a time, many years ago, there was only a channel to interact with a company (what we know asindirect channel). The Mainframe began to rule the world. Developers built programs that called
to routines that called to more programs or routines. Business people was very close to developers and developers could touch any program. The communication flow between Business and IT was
direct.

As everything worked well and it was better using computers instead doing the things manually, more features was added and little by little developers and business people had to work just
in some areas. The knowledge began to be distributed within the company and in consequence, dependencies between areas were more visible. The communication between Business and IT wasn't
so direct anymore and it was necessary put some rules in order to express requirements and features, build the software without breaking anything and promoting to production.

Years later, the raise of Internet made possible other ways to interact with the company: direct channels. With direct channels, business grew exponentially. Companies had to build
applications (mainly web pages) in order to offer some products to their customers. The initial idea was "exposing the Mainframe" to Internet but shortly after, middleware layers were built in order
to orquestrate the invocations to Mainframe and giving the possibility to manage business logic.

More channels mean more functionality, more technologies and platforms, more dependencies, more complexity, more deparments, more people, more rules and process to build software.
New methodologies and complex processes were necessary to get the software deployed in production. Of course there were technical problems as usual but "bureocracy" started to take much
time.

Later on, smartphones and tablets began to be more usual. Again: new devices, new channels, new technologies and tools, more departments, more complexity, more actors, more egos...
And the biggest "problem": time-to-market. At the beginning, time-to-market was something to bear in mind but it wasn't the priority because customers kept using usual channels and they still hadn't
enough trust in perform operations by Internet. Business and IT worked in a separated way, with many problems related to communication.

New paradigms like SOA promised that Business would be allign with IT and everthing should be built following business needs. ESBs, BPMs, Web Services, etc in order to achieve the goal, but
the differences between Business and IT kept existing. Many tools, but many complex processes and methodologies to develop and promote something to production.

Suddenly, customers started to use direct channels more and more and time-to-market became to the first priority. Customers require new services everyday and demand that the services has to works perfectly.
Some companies, like Netflix, show their architectures, tools and methodologies to the world and many companies try to imitate them without success.

In many companies, IT decides that refactoring all the code is the solution. It's necessary to install some tools like Netflix and deploy a lot of services in containers (in a "agile way").
The idea is being able to deploy hundred of times per day to production, like Netflix or Amazon.

But, shortly after, the number of microservices is out of control, there is no ownership, developers do not how to test a feature end-to-end, business people say that IT is a disaster,...,etc.

Some people begin to talk about 'The microservices hell' and the Mainframe rule the world again :) End of the story.



## Why is everything so complicated?

"Do you know how to use Spring Boot? Do you know how to use Eureka? Perfect, you are ready to built microservices. Let's do it".

This is a bad idea.

> __Building "just microservices" is relatively easy. Building a microservices platform is complicated__

Microservices is a concept, a paradigm, a big pattern or a set of patterns. Technology is just a way to perform the patterns but the key is understanding so well what it implies.
A pattern is a "solution" to a common problem. If you don't have that problem, the pattern is not useful for you.

Microservices is about Business. If business people don't help to design the system/platform, your company is going to fail.

Many people talks about "The monolith" referring to a big number of lines of code that must be packaged together in order to work well. You can refactor your code and generate a
serie of services that can be deployed independently. It's not bad because maybe you are going to reduce your technical debt and you are going be able to manage each service individually.
But, for instance...

- What about the ownershipt of the services?
- What about the responsability of the services?
- What about the team responsible for each service? Is it completely autonomous?
- what about the data managed by each service?
- What about the dependencies between services? Are you really sure that you can deploy each service individually?
- What about the procesess to deploy the service to production?
- Are you sure that you really know your business? All the features implemented in the current code are being used by the customers?
- ...

These questions aren't about Spring Boot or Netflix OSS. Here, the important thing isn't how we are going to implement the "service discovery" capability.
Here, the important thing is defining the real business needs and evolving the culture and methodology in order to get a real "end-to-end independent units".

## Your monolith

> __Your "monolith" is not just your code. Your monolith is the set formed by: people and culture, platform, tools and architecture, processes, methodology and government.__

So, what is your monolith? What people usually see is just technology or architecture but the reality is that your monolith is much more:

![Iceberg](/images/monolith/iceberg.png){:height="70%" width="70%"}

If you really want to split your "monolith" you have to make changes in some layers of your organization before refactoring your code or install some tools.
The culture is a key factor. If you don't transform your culture, you're not going to success with "Microservices". Culture is the more powerful strenght in your company.

![Culture](/images/monolith/culture.png){:height="40%" width="70%"}

And you have to think that your company is not Netflix: your company has other problems, other context and other people. So you have to work in order to adapt your culture to the
new challenges (your new challenges not Netflix ones).

At this point, before refactoring everything and adopting the whole Netflix OSS, you need to think about your problems and your goals. What are you pains?

- Do you need to scale up and down some parts of your system because when Black Friday comes your system goes down?
- Do you need different technologies in your ecosystem because some features need to be implemented in a certain technology?
- Have you identified some parts of your system that have much more changes than the others and you need to be splitted those parts?
- Have you identified some parts of your system than need a time-to-market different than the others?
- ...

Maybe, a solution for your problems or needs is going to Microservices or not, but remember, if you decide to go, you have to go as a whole. Applying only technical aspects is not going
to work. Maybe, there are other solutions (not Microservices) that can solve your problems.


## Are you ready for Microservices?

### Think about the real world

Take a minute to think about the real world and how the decissions are made and theirs consequences.

If you're living in a flat, in the middle of the city, you have to follow some rules set by the community, for instance, you can't paint your wall different than the others.
You can not make some changes if the community doesn't accept them. This hasn't to be bad if you don't have problems associated to the location or space or noise, for example.

When you're living in a independent house, you set the rules, you are more autonomous and you can paint the wall and the door of the color you choose. Maybe you have other needs like take your car to go to work.

Living in a flat doesn't have to be better than living in a house ouside the city, depends on your needs. What do you need? Do you need more space? Do you need to be close to the center? There are many reasons to choose one or the other.

But you have to know very clear what you need because if you sell your apartment and you move to a house outside the city without a strong reason to do it, you are going to be frustrated in a short time. If you like noise or you don't like to
drive, you are going to be crazy. If you do it just because it's the edge, you're going to fail.

### Microservices

If you decided to move to Microservices, some interesting questions you have to ask yourself are:

- How are my teams organized? Are they a cross-functional teams?
- How are my business people organized?
- Are business people going to collaborate?
- Are my teams independent?
- How are my communication flows?
- What size are my teams?
- Am I thinking in projects or in products?
- ...

#### Do you know Melvin Conway?

.![Conway](/images/monolith/conway.png)

For instance, a Microservices Architecture without independent and cross-functional teams hasn't any sense. If business people aren't going to collaborate, your microservices haven't got any business ownership...
If you need different teams to develop a Microservice end-to-end, you are going to have many problems and it's better for you keep working as you do currently. For instance, this doesn't work well with Microservices:

.![Non cross](/images/monolith/non-cross-teams.png)

Your teams must have all the necessary skills to build any feature:

.![All phases](/images/monolith/cross-functional-teams.png)

Besides that, your team should be able to design a feature, build it and deploy it to production in a "independent way". If your teams depend of
other departments when they are building the software and try to test or promote to other environments, your Microservices Architecture is going to
fail because you are doing the same as usual but working with distributed systems. So, teams should be autonomous along the whole process:

.![All phases](/images/monolith/cross-functional-teams-2.png)

#### Projects vs Products?

When you're moving to Microservices you must stop thinking in projects and start thinking in products.

The definition of project of PMI is the following:

.![All phases](/images/monolith/project.png)

A project starts with a team and can finish with a different team. Actually, when a project pass to a maintenance, the team responsible for maintaning the result of the project, usually is not the same that
executed the project.

Do you think a Microservice is "something" that has a definied beginning and end in time? If you or your company think so, you would be happy in the hell.

A Microservice is not a project. __A Microservice is the development of a business feature that has to evolve while your company needs or offers that feature.__
The team responsible for the Microservice (from business to DevOps) has to design it, develop it, run it and maintain it util the feature is decomissed. The team knows when the life of the Microservice starts but doesn't know how it's going to dead.
It's like the team's son and the team has to care about it like a son. It's a product that the team offers to customers (other teams, applications, third parties,...,etc).


<br/>
<br/>
I hope you’ve liked this post. In next post we'll talk about a strategies to split the monolith (if you need to do it).

