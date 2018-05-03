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

The most of people, when they are talking about microservices and splitting the monolith, they means just technical aspects:
- Take your code and refactor it in independent services.
- Introduce new tools and concepts like Netflix stack
- Move to a PaaS and use Docker
- Install an Enterprise Event Bus like Kafka or RabbitMQ
- ...

But, do you really think your monolith is only code or tools?


# A short story

I'm going to tell you a short story:

Once upon a time, many years ago, when the customers had just a channel to interact with a company (indirect channels), the Mainframe began to rule the world. Developers built programs that called
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

Some people begin to talk about 'The microservices hell'.

The Mainframe rule the world again :)


# What happens?

__Building "just microservices" is relatively easy. Building a microservices platform is complicated__

Think about the real world. When you're living in a flat, you have to follow some rules based on the community. You can not make some changes in
 the flat if the community doesn't accept them. When you're living in a independent house, you are free to make the changes you want.

![Real Monolith](/images/monolith/real-monolith.png){:height="60%" width="60%"}

__Your "monolith" is not just your code. Your monolith is the set formed by: people and culture, platform, tools and architecture, processes, methodology and government.__

If you really want to split your "monolith" you have to make changes in some layers of your organization before refactoring your code or install some tools.



# Your Monolith
The reality shows that culture is the key factor. If you don't transform your culture, you're not going to success with "Microservices"

![Culture](/images/monolith/culture.png){:height="60%" width="60%"}

Your company are not Netflix: your company has other problems, other context and other people. So you have to work in order to adapt your culture to
 the new challenges (your new challenges not Netflix ones)

So, what your monolith is? What people see is just technology but the reality is that your moolith is much more:

![Iceberg](/images/monolith/iceberg.png){:height="60%" width="60%"}

In this point, before refactoring everything and adopting the whole Netflix OSS, you have to find the best solution for your needs and if the best solution is
 going to microservices, check if your organization is ready for that. For example:

- How are your teams organized? Are they a cross-functional teams?
- How are your business people organized?
- Are your teams independent?
- How are you communication flows?
- What size are your teams?
- ...

<br/>
<br/>
I hope you’ve liked this post. It just my vision about what the monolith is.
.

