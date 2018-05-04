---
author: jaruizes
layout: post
title: "The monolith and the microservices"
date: 2018-05-04 00:30
category : Microservices
comments: false
tags:
 - Digital Transformation
 - Microservices
---

The most of people, when they are talking about microservices and splitting the monolith, they means just "technical" aspects:
- Take your code and refactor it in independent services.
- Introduce new tools and concepts like Netflix stack
- Move to a PaaS and use Docker
- Install an Enterprise Event Bus like Kafka or RabbitMQ
- ...

But, do you really think your monolith is only code or tools?


# A short story

Once upon a time, many years ago, there was only a channel to interact with a company (indirect channel), the Mainframe began to rule the world. Developers built programs that called
to routines that called to more programs or routines. Business people was very close to developers and developers could touch any program. The communication flow between Business and IT was
direct.

Like everything worked and it was better using computers instead doing the things manually, more features was added and little by little developers and business people had to dedicate just
a some areas. The knowledge began to be distributed within the company and in consequence, dependencies between areas were more visible. The communication between Business and IT wasn't
so direct anymore and it was necessary put some rules in order to express requirements and features, build the software without breaking anything and promoting to production.

Years later, PCs and Internet made possible other ways to interact with the company: direct channels. Companies had to offer applications (mainly web pages) in order to offer some products or
services to their customers so they had to "expose the Mainframe" to their customers and invent new products to be consumed in these direct channels. More channels, more functionality, more
technologies and platforms, more dependencies, more complexity, more deparments, more people, more rules and process to build software.

Developing a new feature and promoting it to production began to be very complicated and it tooks too long from the idea to the customer. There were technical problems but the most of time was
consumed in "bureocracy".

Later on, smartphones and tablets began to be more usual. Again: new devices, new channels, new technologies and tools, more departments, more complexity, more actors, more egos... And the biggest "problem":
time-to-market. Until now, time-to-market was something to bear in mind but it wasn't the priority for the customers.

Suddenly customers needs change and time-to-market starts to be critical. Customers require new services everyday and they demand that the services has to works perfectly. Some companies, like
Netflix, show to the world their architectures, tools and methodologies and many other companies try to imitate them without success.

In many companies, IT decides that refactoring all the code is the solution, install some tools like Netflix and deploying a lot of services in different containers (in a "agile way"). The idea is
being able to deploy hundred of times per day to production, like Netflix or Amazon. But, the number of microservices is out of control, there is no ownership, developers do not how to test a
feature end-to-end, business people say that IT is a disaster,...,etc.

Some people begin to talk about 'The microservices hell' and the Mainframe rule the world again :)



# Why is everything so complicated?

"Do you know how to use Spring Boot? Do you know how to use Eureka? You are ready to built microservices". Let's do it. Bad idea.

__Building "just microservices" is relatively easy. Building a microservices platform is complicated__

Microservices is just a concept, a big pattern. Technology is just a way to perform the patterns related to Microservices but the key is understanding so well what it implies. Microservices is Business. If business people don't think anything about
Microservices, your company is going to fail. If business people don't help to design the system/platform, your company is going to fail. If your company don't need Microservices, your company is going be in a big trouble if you transform your ecosystem to
use Microservices.

__Your "monolith" is not just your code. Your monolith is the set formed by: people and culture, platform, tools and architecture, processes, methodology and government.__

If you really want to split your "monolith" you have to make changes in some layers of your organization before refactoring your code or install some tools.
The culture is a key factor. If you don't transform your culture, you're not going to success with "Microservices". Culture is the more powerful strenght in your company.

![Culture](/images/monolith/culture.png){:height="70%" width="70%"}

And you have to think that your company is not Netflix: your company has other problems, other context and other people. So you have to work in order to adapt your culture to the new challenges (your new challenges not Netflix ones)

So, what your monolith is? What people see is just technology but the reality is that your moolith is much more. I think this is what people see and what it's the reality:

![Iceberg](/images/monolith/iceberg.png){:height="70%" width="70%"}

So, at this point, before refactoring everything and adopting the whole Netflix OSS, you need to think about your problems and your goals. What are you pains?

- Do you need to scale up and down some parts of your system because when Black Friday comes your system goes down?
- Do you need different technologies in your ecosystem because some features need to be implemented in a certain technology?
- Have you identified some parts of your system that have much more changes than the others and you need to be splitted those parts?
- Have you identified some parts of your system than need a time-to-market different than the others?
- ...

Maybe, a solution for your problems or needs is going to Microservices, but remember, you have to go as a whole. Only applying technical aspects is not going to work.
Maybe, there are other solutions (not Microservices) that can solve your problems. But, if you decided to move to Microservices, some interesting questions you have to ask yourself are:

- How are my teams organized? Are they a cross-functional teams?
- How are my business people organized?
- Are business people going to collaborate?
- Are my teams independent?
- How are my communication flows?
- What size are my teams?
- ...

For instance, a Microservice Architecture without independent teams hasn't any sense. If business people aren't going to collaborate, your microservices haven't got any business ownership...

Another important thing is that you haven't to refactor everything if it's not necessary. The key is solving problems. For instantce, if you need to scale dynamically some features, you can extract this features to a Microservices and
keep the monolith working.


# Think about the real world

If you're living in a flat, in the middle of the city, sure you have to follow some rules set by the community. You have many facilities but for example, you can't paint your wall different than the others.
You can not make some changes if the community doesn't accept them. But this hasn't to be bad if you don't have problems associated to the location or space or noise, for example.

When you're living in a independent house, you set the rules, you are more autonomous and you can paint the wall and the door of the color you choose. Maybe you have other needs like take your car to go to work.

![Real Monolith](/images/monolith/real-monolith.png){:height="70%" width="70%"}

Living in a flat doesn't have to be better than living in a house ouside the city, depends on your needs. What do you need? Do you need more space? Do you need to be close to the center? There are many reasons to choose one or the other.

But you have to know very clear what you need because if you sell your apartment and you move to a house outside the city without a strong reason to do it, you are going to be frustrated in a short time. If you like noise or you don't like to
drive, you are going to be crazy. If you do it just because it's the edge, you're going to fail.


<br/>
<br/>
I hope you’ve liked this post. It just my vision about what the monolith is.
.

