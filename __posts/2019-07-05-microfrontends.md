---
author: jaruizes
layout: post
title: "Microfrontends"
date: 2019-08-15 01:30
category : Microfrontends
comments: false
tags:
    - microservices
    - microfrontends
---

Today we're hearing "microservices" everywhere. Sometimes the experience is positive, sometimes is negative but the word is in the air. If you don't know what they are, summarizing, this term is usually related to backend architecture and how a system could be decomposed in autonomous and independent pieces, owned and developed by single teams, deployed independently and working all together.

But, when we are developing a product or a feature, we shouldn't forget that the most of them contains backend and frontend services and, if we want to deliver value to our customers we have to deliver end-to-end features. 
Just applying an architectural style to our backend, based on microservices (or not), we won't get enough autonomy to deliver (and maintain) end-to-end features. 

It seems that the next step is being able to delivering value end-to-end. In this context, the term **Microfrontend** really begins to make sense

# Products not just "services"

Usually when we talk about a software product we are talking about something with an user interface (UI) with which an end user interacts. 

The UI hides backend calls to the end user. We understand so well this concept when we're talking about applications we consume, internal or external, but we have more difficult to understand it when we are developing them or when we're talking about frontend and backend worlds. We have to keep in mind that the piece of software we're developing needs other pieces to provide value to the end user. 

If we are building services, we can't deliver them directly to final user because the final user don't expect that and, in the other side, if we're building an UI, we're going to need to consume backend services in order to provide value to end user because the end user expects a dynamic UI (a great UI) showing __real information__.

Well, you can be thinking about APIs and products based on APIs. Your right. This could be a kind of product that a company provide to an other company in order to that company builds an UI over this APIs and provide applications to an end user or only to integrate those two companies. 

The product of the first company is the API but this API, in the most of cases, isn't going to be consumed directly by an end user, so an UI needs to be built becoming a product. The product is offered by the last company but it's an end-to-end product, so we're talking about the same: __providing end-to-end products__.  

| And if we could build independent and fully functional components, composed of all the necessary elements (data, services and user interface), versionables, developed, owned and maintained by a team and integrated at runtime in the application used by end users? They would be like little products |
| :----------------------------------------------------------- |

# Microfrontends: an architecture style

I would like to introduce Microfrontends talking about some principles of this architecture instead of talking about implementations. Why? Microfrotends goes beyond frontend frameworks and their power fight: Angular vs React vs Vue vs ...
Building microfrontends means building end-to-end business pieces to be consumed, in runtime, within a frontend application or even by other microfrontends.

Microfrontends are about an architecture style. Like others architecture styles, it's important to define:

- principles: which are the main principles set in this style of architecture,
- patterns: in which patterns is based on, 
- target: which kind of problems or challenges could resolve and when it's worth applying or not.



Fowler and Lewis wrote a post in 2014 talking about Microservices and what they mean. It was some years ago but I think is a "master post" we always have to keep in mind. So, let's try to apply microservices principles to frontend world:

### Componentization via Services

We're used to build UI components, package them into libraries or packages and publish them in the NPM repository. This means that every application uses these components by importing them in build time. If a component changes, the application has to be rebuilt to get the changes.

Besides that, UI components, normally, are just visual components, more or less complex but they doesn't implement logic or call business APIs. This logic is provided by the parent app. 

So, in this environment, autonomy isn't the main characteristic…But, the idea behind "microfrontends" is just the opposite:

- __what if we'd build "UI Services" instead "UI Components"?__
- __what if we'd build artifacts that encapsulate end-to-end features and we could consume them at runtime by http calls?__

> The idea behind Micro frontends is building "headfull services", that means, delivering end-to-end features by components consumed in runtime by http calls.

Consuming frontends as services means that:

- Micro frontends are developed by a team
- Micro frontends encapsulate backend API calls, so they aren't just UI but they are end-to-end components
- Micro frontends expose contracts as services do, input and outputs.
- Micro frontends are tested individually
- Micro frontends are deployed independently, so it's not necessary to rebult the parent application is something change in the micro frontend



### Organized around Business Capabilities

Micro frontends aren't UI components. Micro frontends means implementing end-to-end business features "as a service" so descomposing the system into business capabilities should be the first step if we want to adopt this architecural style.

We do this exercise when we're defining microservices associated to our system but we do not do the same from the UI point of view and we build the same views in many applications. 

It's also true that in some companies business capabilities are treated from the frontend but sometimes this exercise is done taking just an application and not a system and in other times, frontends are built and packaged into NPM packages and not are consumed in runtime.

In this point, the key is delivering a complete business feature to consumers instead of offering business APIs to the final application implements the UI. Not confusing this with Open APIs.



### Products not Projects

Building Micro frontends means building products, not projects. A team builds and maintain one or more microfrontends of which is the owner. The team is responsible for the "UI Service" over its full lifecycle.

As the Micro frontend encapsulates backend API calls and the user of the Micro frontend only "receives" the UI Service, the team is also responsible to maintain these API calls updated and working. 

Besides that, several versions of a Micro frontend could be published and be consumed, so the team also has to keep in mind this aspect and managing the retirement of versions out-of-date.



### Smart endpoints and dumb pipes

Currently there are a lot of frameworks or products to build frontend applications and its business logic (ok, presentation logic). Communication between components within the application is supported by the framework choosen capabilities. 

In a Micro frontend style, components are designed and developed as decoupled and as cohesive as possible, so components has to be independent, loaded in runtime and communications between components couldn't be supported by a framework. 

Micro frontends communications are supported by DOM standards: html tags, attributes and DOM events, no more. It's possible to use some libraries to abstract the frontend event bus but this tool only has to be used to provide publish/sibscribe capabilities. It means that application logic isn't in the event bus.

Some core actions need to be defined to be implemented in every microfrontend. For instance, actions like language changing to suppont multilanguage sites. Microfrontends should listen to an "language changed" and reacting to this event.

With styling, in a microfrontends world, each microfrontend implements its style and could declare some variables in order to make some customizations. Themes are helpful in these contexts. 



### Decentralized Governance

Similar to Microservices, a centralized governance implies a single technology o framework. Once a framework is choosen then libraries or some components are built to be delivered to development teams in order to get more productivity. When several applications have been developed, changing the framework becomes a big challenge.

With one technology or framework we could have several problems like:

- Not using the best technology/framework to solve a problem
- People gets bore because "it's always the same"
- Locking to a framework, components or even a way (the framework way) to develop.
- Teams not 100% responsible for all aspects of the software they build 

If we can load components in runtime by a http call and these components are used as the same way as other HTML components, why do I have to centralize the technology or frameworks?

Micro frontends associated to business features can be developed with the best technology or framework  according to the complexity, requirements or business context. 

Context is very important because for instance, my company could be in a context where time-to-market is so aggresive and it's necessary to deliver some features to final customer in a short period of time in order to catch those customers. If we can choose a technology or framework that allows us to develop a functional prototype faster than others, let's build that micro frontend with that technology, catch the customer and then, improve the micro frontend in that technology or in other because that micro frontend is loaded in runtime by a http call, there is a contract saying how to consume and the team is the owner.



### Decentralized Data Management

In a Microservices world when we talk about this point we mean how to manage data associated to each micro service:  which database or which model the service is going to use.

In Microfrontends, __data management means backend API calls__. How the microfrontend is going to get its data? Technically speaking you can be thinking about REST or GraphQL for instance, but the key isn't that, the key is getting autonomy end-to-end in order to deliver a complete business feature. 

Patterns like Backend For Frontends are really helpful in this target because if a microfrontend needs to manage data from several domains to solve some business feature, it's necessary a piece to encapsulate this logic. Or for instance, it could be necessary that the micro frontend shows different amount of information depending of the channel.

Security is also in this point. How security is managed for every micro frontend to access to the backend API. In this point, we have to know that the authentication isn't in the micro frontends. Micro frontends are loaded in runtime, dinamically, some of then in public areas and some of then in private areas. They can not implement authentication  logic because they are responsible for other business functionality



### Infrastructure Automation

As microfrontends are independent and fully deployable pieces of software, they also need independent processes for build, deploy and publish. 

Remember that the key principle is autonomy so every microfrontend has to be its own CI/CD process. Within a company could be a common pipeline but depending of the technology it's possible that some changes have to be made to adapt CI/CD processes. 

Teams will also manage their microfrontends in production environments, releasing new versions and maintaining current ones.



### Design for failure

In a microfrontends context, where components are loaded in runtime and backend API calls are managed directly by microfrontends it's important to think what happens if something goes wrong. It's necessary to defing a microfrontend's lifecycle in order to know if the microfrontend is ready to be shown or the parent application (or event the parent microfrontend) has to take additional actions like showing a default component or hidiing this area to the user in order to the user isn't conscious of the fail.

As I said, Microfrontends must be associated to a concrete runtime lifecycle to determine if the microfrontend is ready to be shown or not. For instance:

1. Load microfrontend main file
2. Register component
3. Microfrontend ready event received

Besides that, microfrontends must define a contract in which both input attributes and output events (even exceptions) should be defined. With these tools we can react to failure situations and manage them.



### Evolutionary Design

Working with microfrontends means working with components loaded in runtime, totally decoupled. There is pros and cons in this way of working. A relevant pro is that it's possible to change easily every component without affecting others (keeping the contract). It's also easy technology changes. 

But thinking about how to divide the system is crucial, not considering just one application but a set of domains, subdomains and applications so that microfronteds could be consumed by several applications. 

Build a microfrontend just for being consumed in runtime instead building the same functionality inside the application or in a package, could make sense if that business component has many changes or if it should be implemented in other technology, but if you don't have these kind of problems, only are adding complexity. 




## UI Components VS Microfrontends

It's habitual in many companies having a set of components to be used in the different applications. These components could be from tables, layouts, buttons, inputs, etc to complex headers, tables with a lot of UI functionalities or menus structures. This components can be Web Components and being loaded in runtime but they aren't Microfrontends.

When we talk about Microfrontends we are talking about end-to-end business components:

- UI components, views and behaviours
- Backend API calls
- Logic or State

A Microfrontend is a piece that makes sense for the end user. If the final user access to the Microfrontend directly, the final user gets value from that Microfrontend and he could do a business operation. For instance: 

- Microfrontend - Account Detail: UI views and backend API calls for getting the account info
- Microfrontend - Products Catalog: UI views and backend API calls for showing the products catalog
- Microfrontend - Customer Profile: UI views and backend API calls for managing customer profile

UI Components packaging as Web Components could be used in Microfrontends in order to have a common palette of basics components. Web Components are instantiated in runtime and they could be consumed in every HTML application, so they are framework agnostics
