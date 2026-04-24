---
layout: post
title: "Platforms, DevEx, and many other things to understand (before the AI boom)"
date: 2024-10-28 01:30
image: "/images/pe/intro/pe_intro.jpg"
description: "In this post I provide a summary of the Platform Engineering talk at CommitConf 2024."
tags: [Culture, Platform Engineering, DevEx]
lang: en
ref: platform-engineering
typora-root-url: ../..
---

During 2024, before the AI boom we are currently experiencing, I had the pleasure of giving a talk at **CommitConf** titled **\"Platforms, DevEx, and many other things to understand\"**. If you missed the session or want to review the key points on why *Platform Engineering* is on everyone's lips (and how to avoid it being a resounding failure), here is an \"executive\" summary.

📺 **Talk Video:** [Watch on YouTube](https://www.youtube.com/watch?v=SAeFqfqy0JM)  
📊 **Slides:** [Download PDF](https://jaruiz.io/downloads/commit2024/Plataformas_DevEx_y_otras_muchas_cosas_que_entender.pdf)



## Platform Engineering is nothing new

As I say in the talk, if you've been in the industry for a while, when you start reading articles and diving deeper into this, you'll realize that you've already experienced these types of initiatives, although you probably haven't always known them by this name.

For example, if we look at an important source, such as the ThoughtWorks Radar, we can see that in 2017 this concept was already included in their [radar](https://www.thoughtworks.com/content/dam/thoughtworks/documents/radar/2017/03/tr_technology_radar_vol_16_en.pdf). But, if we look a bit further back, we can see that references to this concept were already being made in 2015:
![platform_eng_referenes](/images/platform/platform_eng_referenes.jpg)

Why is Platform Engineering being talked about everywhere now?



## The problem: the explosion of cognitive load

When I first started professionally in software development, one person could create complete features without managing many tools at once. You don't have to go back to Cobol... For example, if you've lived through the times of Fatwire or had to work with Struts or Spring MVC, one person handled both the view and data access, including SQL queries (so feared today). If there was an error, you went to the log and saw it clearly. If you had to debug, you launched the debugger and did the complete debugging.

Currently, with the evolution of architectures and the separation of layers—for example, SPA, Rest API, etc.—and the \"Cloud Native\" trend (so to speak), a developer handles an ecosystem of many more pieces. Basically, they are asked to know about Kubernetes, Terraform, security, observability, scalability, microservices, event-based messaging, FinOps, ..., etc. In the end, in their daily life, they have to handle a high number of concepts, tools, and technologies, greatly increasing development complexity.

Solving a problem with a very limited number of pieces is not the same as solving it with a high number of pieces.

![platform_eng_referenes](/images/platform/complex_ecosystem.jpg)

The fact that there are so many \"pieces\" is not the subject of this post, but it comes hand-in-hand with the evolution of both business and technology (which came first, the chicken or the egg?). Customer needs have grown exponentially: many more channels available (mobile, web, machine-to-machine, and APIs everywhere, IoT and wearables, ..., etc.), a much greater need or time for \"being connected/informed,\" and a much larger volume of information handled. To solve these needs, the SW development ecosystem has to evolve accordingly.



Therefore, as I've mentioned, the more pieces to handle within the ecosystem, the greater the complexity experienced and, consequently, the greater the cognitive load (mental effort) that has to be managed or supported to carry out a task (**this is where AI is going to help us quite a bit**).

![platform_eng_referenes](/images/platform/cognitive_load.jpg)



On the other hand, the famous ***\"You build it, you run it\"*** philosophy, which was \"coined\" in 2016 by *Werner Vogels*, is powerful, but without the proper support or in \"bad hands,\" it becomes a point of conflict and a way of pointing only to one specific spot: the development team. **The result?** Burned-out teams, constant friction, and a *time-to-market* that doesn't improve.



![platform_eng_referenes](/images/platform/sociedad_codigo.jpg)



At this point, the concept of **Platform Engineering** is born. To understand this concept, the first thing is to understand what a platform is in the context of Platform Engineering.



## What is (really) a Platform in Platform Engineering?

In the talk, I insist that we must understand the concept of \"platform\" within Platform Engineering. When people talk about a platform, they might mean a \"container platform,\" \"infrastructure platform,\" \"API platform,\" \"data platform,\" ..., etc.

**This is not what we understand as a platform in the context of Platform Engineering.**



To me, one of the best definitions of a platform in this context is the one given by \"Evan Bottcher\" (ThoughtWorks) in his article about [Platforms](https://martinfowler.com/articles/talk-about-platforms.html):



> A digital platform is a foundation of self-service APIs, tools, services, knowledge and support which are arranged as a compelling internal product. 
>
> Autonomous delivery teams can make use of the platform to deliver product features at a higher pace, with reduced coordination. 
>
> (Evan Bottcher)
>
>  https://martinfowler.com/articles/talk-about-platforms.html



Therefore, a platform, in the context of Platform Engineering, is a set of:

- **Self-service APIs (portals, CLIs, ...).**
- **Knowledge and support** (the social part we always forget).
- **Golden Paths:** Paved paths that allow teams to be autonomous without having to reinvent the wheel in every deployment.



![platform_eng_referenes](/images/platform/platform_components.jpg)



The platform is managed by the **platform team**, whose goal is to apply engineering practices to design, build, and provide the platform with the most appropriate capabilities at any given time and context.

It must be taken into account that **the clients of this platform and this platform team are the developers**, although the platform team **must be very clear about the context in which it operates**, where there are a series of stakeholders (the CxOs, for example) who will establish constraints, conditions, or make requests. This is, after all, the context in which one works.

The platform team will find itself, on one hand, with its direct clients, the developers, who will have an infinite list of requests, and on the other hand, there will also be a list of constraints (cost, time, team, etc.) and conditions (infrastructure, licenses, etc.) coming from the rest of the stakeholders.

Therefore, **the goal of the platform team and, consequently, of the platform is to offer services that allow developers to do their work more easily within the context in which those teams operate (the company)**.

Working more easily is usually associated with being more efficient and optimal. It's a win-win (employee-company).



> **Key:** Let's not confuse objectives. The objective is not to \"go faster,\" but to \"make it easier.\" Speed is usually a consequence of ease, not the goal itself.



## How to build the platform? Thinnest Viable Platform (TVP)

When building a platform, as with the construction of any product, there are two main paths:

- Believing we know more than potential clients and getting \"down to business\" to build the product *we* want.

- Opting to select potential clients, listening to their needs, and based on that, building the platform, iterating and evolving according to feedback and needs at each moment.

  

The first point is **one of the biggest mistakes usually made**.

In many cases, it's assumed that the needs are clear, a platform team is assembled, and it spends months building \"something\" that developers surely don't need, doesn't work as they expect, doesn't arrive when they expect, and they will end up hating. You can find some cases like this if you look around a bit:



![platform_error_implementation](/images/platform/platform_error_implementation.jpg)



In these cases, **the pattern is usually repeated where the platform is conceived as an end and not as a means to facilitate software development and production**.

To avoid this, an approach we can adopt is the concept of **TVP (Thinnest Viable Platform)**: **building only what is just and necessary at each moment**.



This term comes from Team Topologies and was defined as follows:



> We're not aiming to build a massive platform. We're aiming to build what we in the book call a thinnest viable platform TVP. 
>
> This TVP could be just a wiki page if that's all you need for your platform - it says we use this cloud provider and we only use these services from a cloud provider and here's the way we use them. 
>
> That might just be a wiki page - that might be your platform.
>
> 
>
> (Matthew Skelton, Team Topologies)



**Really, the principle is basic: understand the real needs of your clients at any given time.**

It seems like common sense, but surprisingly, it's not usually taken into account in practice. If your teams only need a well-structured Wiki today, don't force them to use a complex portal. Iterate, ask for feedback, and evolve the platform as a real product.



## Platform as a Product

The TVP approach is still a logical product development approach, even if it's an internal product. When we develop a product, we have to perform these steps continuously:

- Discover and understand the real needs of the clients.
- Incorporate/evolve product capabilities aimed at solving those needs.
- Put it in the client's hands, use it.
- Ask for feedback, draw conclusions, make decisions, and go back to the first point.



In all this process, there is a key role: **Product Manager**. In my opinion, this role must have these characteristics or capabilities:

- Technical component, capable of understanding the needs of the development teams (the clients).
- Social component, capable of understanding the needs of the rest of the stakeholders but also capable of evangelizing in collaboration and in the use of the platform.
- Strategy component, capable of putting all needs together, generating and maintaining a roadmap and product strategy.



## Characteristics of a successful platform

We already know what a platform is and how we can create it, but at this point, as with any product, we have to know if the platform is being a success or not.

Being a product oriented to improve or facilitate software development, it seems clear that the ideal would be not to require a large learning curve to start noticing the gain—that is, the software development process improves and, in addition, it results in greater productivity (when something is easier, more productivity is achieved than when it's very complex). If this happens, then we are making a good product.

On the other hand, if the learning curve is large, we might be adding more complexity (and cognitive load) to the development process instead of reducing it:





![platform_ok](/images/platform/platform_ok.jpg)



To make it a success, there are some key points to consider:

- The platform must be **simple**: it's about eliminating complexity, not adding it. It has a lot to do also with the TVP concept: we aren't looking for quantity but quality.
- The platform must be **usable**: closely related to simplicity but also to understanding and knowing the clients, how they work and develop (this is why the PM must have that technical component).
- The platform must be **transparent**: we must avoid it being a black box. It's a product by and for developers, it has to be open, and we can even make the development teams help evolve the platform through pull requests and similar mechanisms.
- The platform must be **standard**: also closely related to simplicity, usability, and transparency. We don't want to reinvent the wheel, we don't want to create new frameworks by adding abstraction layers over the existing ones. We don't want that. We want it to be as standard as possible because that will allow us more ease to evolve it. For example, if it's \"proprietary,\" we will depend on the knowledge of the people who are on the platform, and the learning curve for new people will be large. Furthermore, if we have built many layers on top of a standard core, if that core changes, we can have quite a few problems to evolve.
- The platform must be **documented**: yes, this is closely related to the previous point and to transparency. The more documented it is (be careful, not quantity but quality), the simpler and shorter the learning curve will be, both for the user and for the people who maintain the platform.



There is one last point that is key: **ACCEPTANCE**: the platform must be accepted, not imposed.

This means that the user must want to use it without anyone forcing them, which is nothing more than saying that they like the product and it helps them in their daily life. When something is imposed and users are forced to use it no matter what, several things happen:

- The previous points (simple, usable, transparent, standard, documented) stop making practically any sense because even if they aren't met, the user is forced to use it. Therefore, the platform engineer doesn't feel forced (what a contradiction) to create a good product.
- Users will resign themselves to using it, but behind the scenes, they will surely start creating their own tools or ways to simplify their work, so the platform will remain only as a \"necessary evil\" that provides no value.

Sam Newman explains it very well:



> Making the platform optional is very challenging for some people. It cost so much, we need to justify the cost. So people have to use it! Otherwise we wasted time and money. 
>
> And as Matthew and Manuel point out, when something becomes mandatory, interesting thing happens. 
>
> When you make people use the platform, you stop caring about making it easy to use, because they don’t have a choice. You aren't incentivised to improve the user experience to attract people to the platform, as they have to be there anyway. 
>
> (Sam Newman)



## The Tech Stack

Although Platform Engineering is not about tools, in the talk we analyze a modern flow that you can start testing today:

1.  **Backstage:** The portal that unifies the catalog and offers *Software Templates*.
2.  **Crossplane:** To manage Cloud infrastructure declaratively (Kubernetes as a control plane).
3.  **ArgoCD:** The GitOps engine that keeps everything synchronized.

I won't go into detail in this post because I think it's well explained in the slides.



## Conclusions

1.  **The platform is the means, not the end.** If the platform becomes more complex than the problem it tries to solve, you have failed.
2.  **The platform must be as large or as small as it needs to be at any given time** (TVP).
3.  **Adoption must be optional.** If your platform is good, teams will want to use it. If you force them, they will look for ways to bypass it (*Shadow Ops*).
4.  **Bottom-up approach.** Listen to the devs before management PowerPoints.



I hope you liked the post. I'll be back with a focus on the AI era!
