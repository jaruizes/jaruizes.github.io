---
layout: post
title:  "Cloud Computing: basic concepts"
date:   2018-04-17 18:30 +0300
image: "/images/cloud-computing/cloud-computing.jpg"
description: "What is Cloud computing?"
tags:   [Cloud]
---

# Context

I would like to start showing you three common scenarios in IT:

### Scenario 1

One of the first question at the beginning of every IT project is where the future application and its components is going to be deployed in production and what requirements is necessary to satisfy in order to keep it running with a high availability and a good user experience. Once the question is answered (with a huge risk component because it just and estimation), the process and the bureaucracy for acquiring and configuring everything starts...

A lot of project time and budget is spent in provisioning resources, licenses and so on and when everything is ready and the new application is deployed for the first time in production,  something goes wrong and the application begins to run slower than it should and suddenly, one of the server goes down. What happens? More machines are needed? More resources (CPU, RAM, storage, network) in each machine? More bureaucracy and more time and budget…

Then, more months later, the number of customer decrees and it’s not necessary so much machines, RAM, storage, etc. More money wasting and people maintaining those machines and software.


### Scenario 2

At the beginning of the project shown in the previous scenario, it’s also necessary provisioning at least two environments (development and preproduction) to deploy the application. What requirements are necessary for each environment? How many developers are going to use the develop environment? It will be enough or it will run too slow?

Infrastructure team has to work in building both environments too and the developers won’t be able to work (well) till the development environment is up and running so the company is, again, spending time and budget in building the environment and then it will spend time and money keeping both environments running.


### Scenario 3

It’s wanted to test a new technology to decide wether making an investment or not. The new technology needs a concrete resources that are not present in the current infrastructure so new resources are buying and configuring only for this PoC, spending time and money for this task. Once the infrastructure is up, the PoC starts but at the end, the result is not good and the investment will not be made.

&nbsp;
# Cloud Computing

What if instead of spending much time provisioning and managing infrastructure resources, could we just push a button and getting those machines and platforms up and running almost immediately? And…

- what if it could be possible to pay only for the time that the resources are being used and then shut them down and left paying for them?
- what if it could be possible to scale up or down your system just with a few clicks or dinamically setting several properties about workload?
- what if it could be possible to create new environments on demand and removing them when they aren’t used?
- …

So, from a bird’s eye view, this is Cloud Computing. It means that

- you don’t need to buy physically hardware or software and store it in your datacenter,
- you don’t need to manage and maintenance all those machines with their main software,
- you don’t need to worry about if your machines are enough good to address days like “Cyber Monday” and even,
- you don’t need an own datacenter

because **an other company do it for you as a service**.

What about money? Theoretically speaking it’s cheaper because you only pay the resources you use (depends of how you manage the cloud and what provider you choose), so for instance, buying a supermachine because you thought that your project was going to need it but then just use a 40% is something that isn’t going to happen because with a few clicks you can scale up or down your system and paying just for the requirements your really need.

So Cloud Computing is a service that helps you to focus just in business by providing exactly the IT resources (hardware and software) you need in each moment.

&nbsp;
# But...where are my server and data?

Everything said till now, sounds very well but, does that means that we are not going to know where my components are deployed?
Many people when talk about cloud, say that the data could be in every place in the world…That’s true, your data, your servers
and your applications can be in any place in the world but you choose where is the right place.

Cloud providers, in order to offer high availability, low redundancy and fault tolerance have data centers located around the world.
They usually manage regions and zones: each region is independent and is located in a separate geographic area (USA, Europe, Asia, Africa,…)
and has multiple and isolate areas called zones. Basically, a zone is associated to a one or more data centers, isolated
from failures in other zones and, a region, is a cluster of data centers.

So when your are designing your cloud architecture, you decide where you want to create your machines. A good practice is deploying your components in several zones
in one or more regions. This is very important in order to prevent fails in a single location that can affect to your business or being closer to your customers giving
them a better user experience.

&nbsp;
# Advantages to move to Cloud

Amazon, in its documentation, identifies very well six advantages of Cloud Computing:

- **Cost efficient**: by using Cloud Computing you only pay when you are consuming resources so it means that you don’t need to make an investment at the beginning of the project buying resources in base of a supposition. The cost now is focusing in the operational phase, when software is really in use.

- **Time to market**: you are going to provision resources and deploy your software much faster than if you have to buy new resources or configure your current resources to add new business solutions.

- **Better prices**: Cloud Computing providers buy and manage resources for a huge amount of customer so they get better prices for the resources that a single company.

- **Focus in business**: by using a Cloud Computing provider you are going to spend much less time provisioning and managing infrastructure resources, base software or backups so you can focus your efforts in business and customers.

- **Closer to your customer**: when your business is global, Cloud Computing helps you to deploy your applications in data centers located around the world with low redundancy and improving your customer experience.

- **Scalability on demand**: it’s so easy to scale up or down your system whenever your business need and you only pay your real requirements

&nbsp;
# Is Cloud so beautiful and perfect?

Cloud is not perfect and everything, it has some drawbacks:

- **Security**: cloud providers are a good target for hack attacks. This is the main concern of the cloud companies but we also have to say that cloud provides better mechanisms to recover from an attack.

- **Internet dependency**: every interaction with cloud providers are based on Internet and sometimes network connectivity could not be the best. So, a good Internet connection is something to keep in mind when
we are going to work with cloud providers.

- **Technical issues**: even the best cloud providers have technical issues that can affect to the service. For that reason, it's important to choose a good cloud architecture and strategy deploying our applications in several
zones or regions.

- **Legal issues**: storing data in the cloud could have associated legal requirements that our company has to fulfill. When we manage sensible data is very important to know what the security best practices are
and if we are allowed to manage or store data outside of its origin country.

- **Vendor lock-in**: migrating from one platform to another could be very difficult if our cloud provider: proprietary formats to store data, proprietary tools or platforms…,etc.

&nbsp;
# Cloud layers

To finalize this general post, once we know what Cloud Computing is and its pros and cons, we need to know that there are three “layers” (or types) in Cloud services:

- **Infrastructure as a Service (IaaS)**: it’s the bottom level of cloud and it includes services like virtual machines, servers, storage, load balancers, backup, and security. Basically,
the cloud provider provides the infrastructure to you and you have to install on top of it the software you need for your business. Examples of this are: Openstack, some AWS products like Amazon EC2, Amazon S3 or
Google Cloud products like GCE

- **Platform as a Service (PaaS)**: it includes capabilities to develop, deploy, execute and manage your apps. Openshift, CloudFoundry or Heroku are good examples of this concept.

- **Software as a Service (SaaS)**: it includes software that you can use directly for your business: Office 365, Salesforce, Google Apps….

- **Function as a Service (FaaS)**: it provides everything you need to execute pieces of code (functions). You just worry about your code, anything else: no servers, no infrastructure, scaling, etc...


&nbsp;
# Do I have to move everything to Cloud?

Moving to Cloud is a big step for companies that have a lot of systems on-premise so, the strategy has to be move to Cloud step by step, not
a big bang.

The first step usually is using Cloud as store provider for some data, synchronizing or migrating on-premise data to cloud data, removing some on-premise
database instances.

Rehosting some machines to resources in the cloud could be also an initial step. Cloud providers offer some services to import/export virtual machines from one system to the other one.
When your are rehosting your applications it's a good moment to redesign its architecture taking advantage of cloud services and new architecture models like microservices. By Virtual Private
Clouds, companies can integrate systems on cloud with systems on-premise building a common network and also, it's possible to have a dedicated line between cloud data center and its
own data center. This is called as Hybrid Cloud because some components go to the cloud while others are kept on premise.

By last, there could be some applications that can not move to cloud for legal reason or simply because the company prefers keeping them in its datacenter.


<br/>
<br/>
I hope you’ve liked this post. I’ll try to detail the main cloud providers and its services (Amazon Web Services and Google Cloud) in next posts.




