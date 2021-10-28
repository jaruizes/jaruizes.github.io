---
layout: post
title:  "Thoughts about Microfrontends"
date:   2019-10-23 14:30 +0300
image: "/images/microfrontends/header.png"
description: "This post maybe is too long and I could write several posts but I considered a good option to write all I think about Microfrontend and MicroX architectures in just one post, like a book."
tags:   [Microfrontends]
---


This post maybe is too long and I could write several posts but I considered a good option to write all I think about Microfrontend and MicroX architectures in just one post, like a book. This post is a "living-post"...

Have you heard the term "Microservices"? Sure. Microservices are everywhere. Sometimes the experience is positive, sometimes is negative but "Microservices" are there. This concept is usually related to backend architecture and talking about how a system could be decomposed in autonomous and independent pieces, owned and developed by single teams, deployed independently and working all together.

But, how is this valuable for the final user or customer? When we are developing a product or features, we shouldn't forget that the most of features contains backend and frontend parts. If we really want to deliver real value to the customers, we should deliver end-to-end features within a team. 

I would like to show [this tweet from Sam Newman](https://twitter.com/samnewman/status/1167062137006645249):

![Sam Newman Tweet](/images/microfrontends/newman.png)

Having dedicated teams to frontend or backend layers isn't efficient and productive. Applying an architectural style just to backend (based on microservices or not) or trying to be organized in teams with no end-end skills, we won't get enough autonomy to deliver (and maintain) end-to-end features and provide value to the final user.

What about Business? Business is changing everyday, customers are demanding more and more digital processes. How can companies know how their business needs will be in a few months?. They don't. 

> Companies doesn't need static architectures. They need dynamic architectures based on independent and decoupled pieces to build end-to-end solutions for each moment. These architectures have to be end-to-end architectures and must be technology agnostic in order to be able to evolve easily according to business needs and the evolution of the technology itself.

In this context, the term **Microfrontend** really begins to make sense. In this post I'm not going to talk about technical implementations about Microfrontends (Zalando, DAZN, Ikea...) because I want to express my (logical) perspective about them.

<br>

# Build products, not just "headless services"

If you think about software products from an user perspective, for sure you are thinking about applications where you perform some business actions like making a purchase, ordering a transfer or booking an hotel. You use these applications through the user interface and you don't care about what is behind that UI, do you? For instance, when you use your banking application to check your global balance or last movements you only interact with the user interface, not with the services behind that UI. You want the application to work well, just that.

As final user, you don't care If your bank release a new version of backend payment service or a new version of some frontend components. A final user demands an end-to-end solution or product where frontend and backend pieces works together:

- If the UI is great but backend services don't work well (or not exist) the UI will not provide value to the user. 
- If backend services work well but there is no UI or the UI doesn't work, the system will not provide value to the user. If several applications have similar business need (features) and the UI looks different in each one or works differently (because UI or services), the user experience is so bad
- If data managed by services and UI is not a valid information to the user or it hasn't enough quality, the value for the user is so poor.

![why_microfrontends](/images/microfrontends/products.png)

So, in my opinion, "Microservices" are the beginning but they are not enough to deliver value. The truth is that if we want to provide business value to end users we will need a good user interface working with good services and good data like a whole. Deliver value means deliver software products or end-to-end components.



## End-to-end perspective

Many companies have started to modernize their architectures in order to build better applications, more scalables and more evolvables. Some of theses companies use a Microservices style, others have decided to return to monoliths but building "better monoliths" and others are just thinking about how improve the way to build software. 

The most of them have something common: they think about services, decomposition in pieces, independent teams, agility, etc but the most have started just focusing on backend systems (APIs, backend services, migration HOST to (micro) services, etc...). 

But, as we have seen in the previous section, something is true: the most of features are end-to-end and they are  composed for elements in every layer:

![focus_in_backend](/images/microfrontends/focus_in_backend.png)

So, taking an approach only focused in backend services (or systems) is not enough efficient and productive:

- If you build wonderful (backend) services around business capabilities but you don't build an UI associated to those business capabilities your will not be building unique business capabilities. You will be building differents flavours of the same business capability because you will build several UIs in different applications to perfom the same business capability (or very similar)  

  ![feature-different-views](/images/microfrontends/feature-different-views.png)

  You are building **"headless business features"** and you have to develop "heads" in order to provide these features to the final users. 

  For instance, in a banking environment, why do you have to develop the account movements view in the main consumer application and you also develop a similar view in the backoffice application or in another application also used by the customers? 

  

- If you achieve a great autonomy in backend systems but you don't do the same in the frontend apps, that means that your (backend) autonomy is not real because you can not deliver end-to-end features to the end user without depending others. 

  ![autonomy](/images/microfrontends/autonomy.png)
  
  
  
- What about Data? If you don't treat business capabilities as end-to-end features it's possible (or very likely) that your data is replicated in several systems, adding complexity, redundancy, security risks, etc...

It seems that building end-to-end features leaded and owned by a unique team would be more efficient, isn't it? 

![end-to-end-features](/images/microfrontends/end-to-end-features.png)

If one team is able to develop all the necessary elements for deliver a feature, 

- autonomy is great because the team doesn't depend on others
- the feature is owned by a team (functionally and technically)
- quality is applied end-to-end

<br>

## Keep the business features inmutables and reuse them

Imagine this situation. Maybe it's not the best approach to organize a company architecture but it could be something real in many companies:

![example](/images/microfrontends/situation-example.png)

In this scenario, we can see two applications consumed by different users: 

- Customers: application in which customers (final users) perform business actions. 

- Customer Care: application used by employees to help to their customers. This application tries to be similar to the Customers application in order to give a good service to the customer.

There are many ways to implement this scenario: one approach could be that both applications have their own backend for frontend in order to orchestrate calls to different services and manage details regarding to different channels and different frontend developments are built in each application. Other approach could be to build a frontend module containing the functionality and this module is integrated in both applications. The backend for frontend usually depends on the application and it isn't reused and backend services are the same in both applications. In other companies, there will not be backend for frontend and frontend applications will consume directly backend services.

In all the approaches, backend services are uniques and developed by an specific team but frontend parts are not uniques and they are developed by different teams. If a backend service change and a new version is released, the backend for frontend or the frontend will consume this new version of the service. 

So, business capabilities provided by backend services owned by an specific team could be considered as **inmutables**. Frontend implementations of the same functionality across different applications are considered as **mutables**

> If the implementation of a complete business features between applications is not considered as a "product" and their components (services, frontend, etc) are developed by different teams, they are considered **mutables** from an end-to-end point of view.

That means they are differents implementations of the same business capability:

![mutable features](/images/microfrontends/mutable-fetatures.png)

The ideal situation would be that the business feature was reused from the top layers to the bottom layers, but in some cases you are not responsible for all the elements (for instance external services). The target is to build end-to-end blocks of business capabilities to be reused. 

As we do in backend part, it we can isolate business capabilities in the frontend part (UI and Backend For Frontend), consuming instances of these business capabilities within the applications, calling the same backend services and releasing new versions when something changes, **we'll also be building inmutables business capabilities in the frontend layer and the end-to-end could be considered inmutable**:

![inmutable features](/images/microfrontends/inmutable-fetatures.png)

<br>

# Microfrontends: fully business components

As I'm saying in the previous sections, **the target is to build end-to-end business components** that applications can load in a decoupled way (by a http call) and technology agnostic. 

If we could build fully business components, independent and composed of all the necessary elements, versionables, developed, owned and maintained by a team and loaded and integrated at runtime in the application, we will be building little end-to-end products to be delivered to the different applications that need to include these business features.

The following picture summarizes the idea behind this concept:

![microfrontends-idea](/images/microfrontends/microfrontends-idea.png)

<br>

## So, what is a Microfrontend?

First at all I have to say thay I don't like the term "Microfrontend" (the same as Microservices). This term is associated only to frontend world and this is so wrong. The idea is **providing "headfull" business services instead just a backend services or "headless" services**. So, when we say "Microfrontend" we mean **an unique end-to-end business component to be called and  instantiated at runtime by the frontend part of the different applications**

Considering this perspective, obviously, **the main part of a microfrontend is the frontend part** but not the only one. This part is what will be consumed and loaded by applications or another microfrontends but in order to get fully business capabilities, calling to backend services will be necessary. How is it managed? Here, there are several possibilities:

- Building a backend piece called **Backend for frontend** (BFF)) in order to manage calls to business API, orchestration, information adaptation to the channel,...,etc. This piece will be also part of the microfrontend, sharing ownership. This approach will be the most usual because in real systems, orchestration of services is very common in the most functionalities.

- Access directly to a business service already implemented in the same domain or in different domains or event external. In this case, the microfrontend is the part that is exposed to the consumer (it's the product), so it has to guarantee everything works. 

  If the services consumed by the microfrontend change, maybe the frontend part of the microfrontend (and the one) will have to be updated relasing a new version of the microfrontend. If services are in the same domain or have the same owner it will be easier to keep the microfrontend updated than if the services are in other domains or they are external. 


So, in the most of cases a microfrontend will be composed by:

- An User Interface implemented in any frontend technology or framework supporting to be consumed by "an http call".

- A Backend for Frontend implemented in any technology that supports interaction with the UI component, the channels and the different backend services. It also manages the first level of security and the access to the business APIs

It's very important to consider all the components associated to the microfrontend as a whole. That means that everything has the same owner and is released at the same time, as a product:

<img src="/images/microfrontends/structure-basic.png" alt="basic structure" title="Microfrontend Basic Structure" width="480" height="320" />

<br>

## Loaded and integrated at runtime (like services)

I want to write a section dedicated to this point because I think is a very important point when we talk about Microfrontends. This is the key when we talk about independent and autonomy components. The devil is in the detail. I'm going to try to explain comparing rest services with modern frontend applications.

First, think about how **Rest services** are consumed by the applications or even another services:

- There is a contract where the endpoint information is declared: request, response, security if needed, etc...
- Consumers only send an HTTP call to an URL as the service contrat says and wait for a response. Consumers doen't know any detail about the internal implementation of the service or how the service manages its data. Languages/frameworks can be different between consumers and service.
- Consumers are deployed in a different server that the service artifact
- If the service needs to be updated by some reason (fix a bug for instance), the application doesn't need to be rebuilt and redeployed to get the changes.

Now, think about how **modern frontend apps** works:

- The application is coded in a specific language/framework, mainly javascript
- The application can be divided in components and components can be loaded on demand, at rutime, if the user navigates to the view using those components
- The application needs to be packaged with its components although they can be loaded at runtime (on demand) or all together when the application starts
- The components and the application are deployed in the same server, as a whole
- If a component needs to be updated by some reason (fix a bug for instance), the application needs to be rebuilt to package the new version of the component and redeployed. 

These models are similar but with little differences: 

- a REST service is decoupled from the client application because it is consumed by a HTTP call instead being included in the application package. 
- the Rest service exposes a contract where it specificities input parameters, output structure and error codes.
- the Rest service maybe can be implemented in a language totally different of the frontend applications or the other Rest services, but they interact by HTTP calls

> Why don't do the same with the frontend components?

<br>

## Events

We're talking about a fully decoupled pieces in a frontend application. These pieces are independent and each of them implement a business capability but there are some scenarios when an action in a business component fires another action in other component. 

Imagine an online shop. The catalog could be implemented by a Microfrontend and it manages everything related to show the products to the user. When the user click the icon "add to cart", the Microfrontend implementing the cart capability has to be notified that a product needs to be added to the cart. But, maybe others Microfrontend want to be notified too (recent products added, history, etc...)

The way to notify these actions shouldn't be imperatively, that is, the catalog component calling other components directly. Why not? Because the catalog should have to know which are the rest of the components and which components need to be notified and how (calling a public method) and once again, we'll build a full coupled system. The idea isn't this. 

The idea is that components should be totally independent, that means that they don't know which other components are loaded or if they have to call to concrete component when something happens. When something (important) happens, an event is sent and other components can listen to these events and react to them. These events contains information about the action performed and the component who has fired it.

<img src="/images/microfrontends/event-bus.png" alt="event bus" title="Event Bus" width="480" height="320" />



### What is important and should be notified?

Depends on your system or applications and your business. What isn't important today could be important tomorrow. By this reason is so important that components are totally decoupled by using events. 

In this kind of architectures, design exercises are fundamental because it's necessary to model which events need to be notified, their information and who is going to react to them and how.

That adds complexity to the system because it's more difficult to trace actions and to know the state of the system. 

<br><br>

## Where is the state?



The state? Each Microfrontend has to own state but the application composed by some Microfrontends and other pieces (no Microfrontends) has its state. 

The state within a Microfrontend is controlled independently by that Microfrontend and it's doesn't care to the main application. This state changes by the events heard by the Microfrontend. The state of the main application is the state associated to the Microfrontend choreography and it's complex to manage.

<img src="/images/microfrontends/state.png" alt="state" title="State" width="480" height="320" />

Once again, design is so important. Time to design and design well is fundamental. You are going to fail if you don't take time to think about the system, its events, its components and how everything is going to work together.

<br>

# Microfrontends and Microservices principles

When we talk about Microfrontends (or Microservices) we are talking about a way to build complex systems and how to structure the different pieces and their interactions. We don't talk about concrete technology. By this reason, Microfrontends goes beyond frontend frameworks and their power fight: Angular vs React vs Vue vs ...

> Building Microfrontends means adopting an **archytecture style**, building and delivering end-to-end business pieces, defined by a formal contract and with a clear ownership, packaged and deployed independently, to be integrated and consumed at runtime within a frontend application or even by other microfrontends.

Like some architecture styles, it's important to set:

- which **kind of problems or challenges could resolve** and when it's worth applying or not.
- which are the **main principles and patterns**
- which **cultural and methodology changes** are required (maybe a changes in your company will have to be performed)

[Fowler and Lewis wrote a post in 2014 talking about Microservices](https://martinfowler.com/articles/microservices.html) and what they mean. It was some years ago but I think it is a "master post" we always have to keep in mind. In this post, nine principles are set:

- [Componentization via Services](#compservices)
- [Organized around Business Capabilities](#businesscap)
- [Products not Projects](#products)
- [Smart endpoints and dumb pipes](#endpoints)
- [Decentralized Governance](#governance)
- [Decentralized Data Management](#data)
- [Infrastructure Automation](#infrastructure)
- [Design for failure](#failure)
- [Evolutionary Design](#evolutionary)

Let's try to apply microservices principles to frontend world:

<br>

### <a name="compservices">Componentization via Services</a>

If you are using a modern frontend framework probably you're used to build UI components, package them into libraries and publish them in the NPM (or bower) repository. This means that every application uses these components by integrating them into the main application in build time and packaging all together in an unique package (although you are using lazy loading and components are loaded on demand). 

If a component changes, the whole application has to be rebuilt to get the changes and redeployed. So, in this scenario, autonomy isn't the main characteristic. 

**Applications are built as a Lego system with a hard unions between them.** If you are building a house with Lego pieces and you need to change some part of the house, you'll have to "rebuilt" the house.

<img src="/images/microfrontends/frontend_as_lego.png" alt="components as lego" title="Components as Lego" width="480" height="320" />

The idea behind "microfrontends" is just the opposite:

> __what if we could build artifacts encapsulating end-to-end features and we could consume them at runtime by simple http calls?__

Componentization frontends as services means that:

- Microfrontends are developed and owned by a team
- Microfrontends expose contracts as services do, input and outputs, events and styles.
- Microfrontends are tested individually
- Microfrontends are deployed independently in a "Microfrontend server". They are not packaging within the main application, so it's not necessary to rebult the main application if something changes in the Microfrontend
- Microfrontends encapsulate all the backend API calls they need, so they aren't just UI. They are end-to-end components

![microfrontend basic structure](/images/microfrontends/frontend_as_services.png)



##### Tip for Java developers

If you use Maven, the most of the libraries are integrated in build-time and everything is packaged in the same artifact. If a dependency changes, rebuilt and repackage is necessary. 

In Maven, you also find dependencies with "provided" and "runtime" scope. Dependencies tagged with "provided" scope are needed during the build phase but they will not be packaged because they will be provided by the execution environment (usually an application server). Dependencies with "runtime" scope are not needed during build time but during the test or runtime phase.

"Runtime" scope is similar to the target of Microfrontend: not need dependencies at build phase, not package all the pieces within the parent application but being consumed at runtime

<br>

### <a name="businesscap">Organized around Business Capabilities</a>

Microfrontends aren't just UI components. Microfrontends means implementing end-to-end business features "as a service". By this reason, descomposing the system into business capabilities should be the first step if we want to adopt this architectural style.

> The need to build a Microfrontend has to have its origin in a business need. It should not exist a Microfrontend without a business origin and without an owner from the business team. Building Microfrontends is not a refactor technique in which technical people extract pieces from frontend applicarions and expose them to be consumed as HTTP calls.

Business doesn't mean just final customer. Business could be an internal need from some department that could be potentially defined as "microfrontend". 

When I talk about "business need" I mean "business need" within a company not within an application. Building an application decomposing it in components and exposing them as Microfrontends without keeping in mind other applications within the company only it will introduce complexity to that application. 

> Defining Microfrontends has to be a global exercise, taking into account the set of business needs within the company and how business artifacts could be reused by the different applications. 

It's true that in the most of companies there isn't a green field and all the business needs are not always known when you are building applications. By this reason I recommend a "monolith first approach" and a set of business owners that have the global knowledge of the set of applications built in the company in order to determine when it's necessary  to extract a concrete functionality to a Microfrontend. 

<br>

### <a name="products">Products not Projects</a>

Building Microfrontends means building full products, not projects. A team builds and maintains one or more microfrontends of which is the owner. The team is responsible for the Microfrontend over its full lifecycle.

A project starts with a team but it can finish with a different team. Actually, when a project pass to a maintenance, the team responsible for maintaning the result of the project, usually is not the same that executed the project.

Do you think a Microfrontend is “something” that has a defined end in time? If you or your company think so, you would be happy in the hell.

A Microfrontend is not a project. **A Microfrontend is the development of a business feature that has to evolve while your company needs or offers that feature.** The team responsible for the Microfrontend has to design it, develop it, run it and maintain it util the feature is decomissed. The team knows when the Microfrontend births but doesn’t know how it’s going to dead. It’s like the team’s son and the team has to care about it like a son. It’s a product that the team offers to customers (other teams, applications, third parties,…,etc).

As the Microfrontend also encapsulates backend API calls and the user of the Microfrontend only "receives" the UI piece, the team is also responsible to maintain these API calls updated and working.

![microfrontend basic structure](/images/microfrontends/products-vs-projects.png) 

Besides that, several versions of a Microfrontend could be published and be consumed, so the team also has to keep in mind this aspect and managing the retirement of versions out-of-date.

<br>

### <a name="endpoints">Smart endpoints and dumb pipes</a>

There are a lot of frameworks or products to build frontend applications or components. Communication between components within the application is performed following the rules set by the framework choosen. So, applications and components are not built as a endpoints but they are built as a pieces integrated within a parent application.

In a Microfrontend style, components are designed and developed as decoupled as possible, so components has to be independent, loaded in runtime and communications between components couldn't be supported by a framework. 

Microfrontends communications must be supported by DOM standards: html tags, attributes and DOM events. It's possible to use some libraries to abstract the frontend event bus but this tool only has to be used to provide publish/sibscribe capabilities. Application logic never is in the event bus.

Microfrontends have a defined responsibility, that means that a Microfrontend is designed to solve a concrete business need not a set of them. 

<br>

### <a name="governance">Decentralized Governance</a>

A centralized governance usually implies a single technology o framework. Once a framework is set, libraries or some components are built to be delivered to development teams in order to get more productivity reusing components and libraries between applications. Time after, when several applications have been developed, changing the framework becomes a big challenge.

Choosing just one technology or framework has some limitations like:

- Not using the best tool to solve a problem
- People gets bore because "it's always the same"
- Lock-in to a framework, components or even a way (the framework way) to develop.

> If we could load components at runtime and these components were used as the same way as other HTML components, why would I have to centralize the technology or frameworks?
>

**So adopting Microfrontends doesn't mean adopting one framework or technology**. 

> It's adopting a way to build UI Services, technology agnostic, that can be consumed at runtime by any application, similar to backend services (http) are consumed.

Microfrontends can be developed with the best technology or framework according to the complexity, requirements or business context. 

This doesn't mean that there is no Governance. Governace means principles, rules, patterns,...,etc but not technical implementations. Usually, some "core actions" need to be defined to be implemented in every microfrontend. For instance, actions like language changing to suppont multilanguage sites: your company can set the principle that every Microfrontends should listen to an "language changed" event and reacting to it.

Similar with Security concerns. This needs to be defined globally and teams in charge of microfrontends must follow the patterns and rules.

<br>

### <a name="data">Decentralized Data Management</a>

In Microservices, when we talk about this subject we mean how to manage data associated to each microservice:  which database or which model the service is going to use.

In Microfrontends, __data management means "backend API calls"__. How the microfrontend is going to get its data? Technically speaking you can be thinking about REST or GraphQL for instance, but the key isn't that, the key is getting autonomy end-to-end in order to deliver a complete business feature. 

Patterns like Backend For Frontends are really helpful in this target because if a microfrontend needs to manage data from several domains to solve some business feature, it's necessary a piece to encapsulate this logic. Or for instance, it could be necessary that the microfrontend shows different amount of information depending of the channel.

Maybe you are wondering about security and how the microfrontends get their data in a secure way. Microfrontends are loaded at runtime, dinamically, some of then in public areas and some of then in private areas. To access this private areas is neccessary that the user is authenticated. This is responsability of the main application, not of the microfrontends. 

Microfrontends need to know if the user is athenticated and how to get the tokens (or whatever you use) in order to invoke backend APIs. In this point, two strategies are possible:

- The main app intercepts all the backend calls and adds the security headers so microfrontends don't have to implement it
- Microfrontends are allowed to get the tokens received when the user is authenticated and they are responsible for generating the security headers they need to access to the backend services.

<br>

### <a name="infrastructure">Infrastructure Automation</a>

As microfrontends are independent and fully deployable pieces of software, they also need independent processes for build, deploy and publish. 

Remember that the key principle is autonomy so every microfrontend has to be its own CI/CD process. Within a company could be a common pipeline but depending of the technology it's possible that some changes have to be made to adapt CI/CD processes. 

Teams will also manage their microfrontends in production environments, releasing new versions and maintaining current ones.

<br>

### <a name="failure">Design for failure</a>

In a microfrontends context, where components are loaded in runtime and backend API calls are managed directly by microfrontends it's important to think what happens if something goes wrong. It's necessary to defing a microfrontend's lifecycle in order to know if the microfrontend is ready to be shown or the parent application (or event the parent microfrontend) has to take additional actions like showing a default component or hidiing this area to the user in order to the user isn't conscious of the fail.

As I said, Microfrontends must be associated to a concrete runtime lifecycle to determine if the microfrontend is ready to be shown or not. For instance:

1. Load microfrontend main file
2. Register component
3. Microfrontend ready event received

Besides that, microfrontends must define a contract in which both input attributes and output events (even exceptions) should be defined. With these tools we can react to failure situations and manage them.

<br>

### <a name="evolutionary">Evolutionary Design</a>

Working with microfrontends means working with components loaded in runtime, totally decoupled. There is pros and cons in this way of working. A relevant pro is that it's possible to change easily every component without affecting others (keeping the contract). It's also easy technology changes. 

But thinking about how to divide the system is crucial, not considering just one application but a set of domains, subdomains and applications so that microfronteds could be consumed by several applications. 

Build a microfrontend just for being consumed in runtime instead building the same functionality inside the application or in a package, could make sense if that business component has many changes or if it should be implemented in other technology, but if you don't have these kind of problems, only are adding complexity. 

<br>

<br>

# UI Components vs Microfrontends (Business Components)

We're used to work with UI Components. The most of companies have developed a set of UI components, from simple inputs to complex tables or elements. We build complex components or features using these UI Components because these UI Components don't make sense by themselves for the final user. 

Something make sense to the final user if it has an UI and manages Data. If the final user could see just the UI Component used in the "Movements table", he would see a dummy or a empty table and he couldn't perform any business operation over that component.

> A Microfrontend is a piece of software that makes sense for the end user by itself. If the final user could access to the Microfrontend independently, the final user gets value from that Microfrontend and he could do a business operation.

For instance: 

- Microfrontend - Account Detail: UI views and Backend for Frontend performing the necessary API calls for getting the account info
- Microfrontend - Products Catalog: UI views and backend API calls for showing the products catalog
- Microfrontend - Customer Profile: UI views and backend API calls for managing customer profile

> An UI Component doesn't make sense to the end user because it doesn't manage data by itself. Usually, calls to backend services are performed outside these UI Components. 

UI Components could be part of the visual layer of a Microfrontend. Within a Microfrontend, those UI Components plus backend components acquire real business capabilities to the final user:

![microfrontend-vs-uicomponents](/images/microfrontends/microfrontend-vs-uicomponents.png)

<br>

### Web Components != Microfrontends

You can be thinking about Web Components as Microfrontends. It's true that a Microfrontend is basically loaded like a Web Component by the parent application, using it like other HTML tag. But, how is the component integrated in the parent application. Buid-time? Runtime?  

In the most of cases, the approach to use Web Components is mainly by NPM (or Bower) packages and : 

- they need to be declared in development time (package.json / bower.json), 
- they need to be downloaded in development time
- they need to be packaged and deployed with the application 

For instance, __[Webcomponents.org](https://www.webcomponents.org/introduction)__ and __[LitElement](https://lit-element.polymer-project.org/)__:

![why_microfrontends](/images/microfrontends/webcomponents-publish.png)

This approach isn't the ideal one because there is a "strong" coupling between the application and its components. 

> The target is being able to consume fully functional components like services without packaging them inside the application

Web Components standard is the way in which we can develop Microfrontends but if they don't have business sense or they are not integrated at runtime, 

<br>

# Visual concerns 

When you listen the term "Microfrontend" for the first time maybe you wonder:

- Responsive? Is this responsive? Mobile first?
- Are they "static"? If do we need to change some visual properties depending on the "parent application"?

Well, **those questions are not about Microfrontends. They are about UI components.**

Think about your UI catalog components and its complex components. They are designed thinking about responsive concerns or if they are going to be used in mobile applications or not. Does your company have UI components designed for mobile applications? If it does, you could build microfrontends over them

> A Microfrontend could have several views depending of the channel it was instantiated. The restriction is all those views belong to the same logical piece, are owned by the same owner (business and technical) and provide the same business functionality in order to be reused in another applications.

<br>

#### Themes

Microfrontends don't have to be static and closed pieces from a visual point of view. They could declare some properties in order to customize their aspect or appliying themes. 

Custom CSS properties are very helpful to achieve this capability. It's possible create **themes** grouping different customizations, changing colors, fonts, icons.... Applications can apply these themes and the microfrontends instantiated within them will take the visual aspect expected. For instance, we could design light and dark themes to be applied to microfronteds. 

<br>

# Microfrontends contract

If we want to treat Microfrontends as services we need to define a contract to be used by the consumers to work with them. What should a Microfrontend define?

![contract](/images/microfrontends/contract.png)

- Basic data / metadata: name, description, owner, area
- Attributes: input parameters to be set when the microfrontend is used
- Custom visual properties: which visual variables could be modified
- Events: 
  - Which events is it listening to
  - Which events are firing and when 

As the Microfrontend hides backend API calls, anything more isn't necessary for the customer in order to use the Microfrontend

<br>

# Architecture

In this section I would like to show a basic architecture to get the main targets. The main targets to archive are:

- Components developed and deployed by independent teams
- Not just one technology or framework to develop
- Components consumed at runtime by an http call by any HTML & Javascript application

How can we achieve these targets?

<br>

## Core components

#### Microfrontends Registry Server

The first problem to solve is how distributing the components to achieve autonomy and independent deployment in order to be consumed by applications. How will an application know where the Microfrontend is? 

Imagine that each Microfrontend is served from a different server. Applications would need to storage all these URLs servers in order to consume them. What if a new Microfrontend is deployed? Does the application has to add the new URL in its config file? Think about you have many applications and a good number of Microfrontends. This isn't scale.

We need an "external" piece that I call "Microfrontend Registry Server" (MRS). This piece is responsible for serving Microfrontends to the applications when they are requested. By this reason, it's also the place where teams deploy their Microfrontends. Applications only need to know where the Microfrontend Registry Server is (one URL) to consume any Microfrontend. If a new Microfrontend is deployed, applications doesn't have to do anything in order to get it. 

![registry server](/images/microfrontends/registry_server.png)

This piece can be so simple or complex. For instance:

- **Microfrontend Versions**: this piece can allow just one version of a Microfrontend or the possibillity of storaging and serving different versions of a Microfrontend
- **Security**: this piece can serve any Microfrontend requested by any application or, for instance, implementing a security mechanism consisting on rules so that a Microfrontend only can be consumed by authorized applications
- **Storage**: this piece can be so simple that teams publish a ZIP file containing all the Microfrontend files and the ZIP is extracted inside the Registry Server to be served or by the opposite, the files associated to a Microfrontend can be storaged (deployed) in its own server and the MRS acts like a proxy in order to serve the Microfrontends to the consumers.

I'm not going to concrete details about implementation of this piece because it could be implemented in any technology or even using existing tools like, for instance, a NGINX. 

<br>

#### Microfrontends Loader

If we want to load Microfrontends at runtime inside the applications we need a component or piece doing this capability. This piece is responsible for calling to Microfrontend Registry Server in order to get a Microfrontend (and its version if the MRS support this feature). 

![microfrontends loader](/images/microfrontends/mf_loader.png)

This piece,

- Performs calls to MRS in order to get the microfrontends required by the application
- Loads the main file of the Microfrontends inside the application
- Assigns an unique identificator to microfrontends instances
- Sets the initial attributes to microfrontends
- Manages the microfrontends lifecycle 

<br>

#### Event bus

This conceptual piece is responsible for providing channels used to communicate the different independent components (Microfrontends) loaded in the application. This piece doesn't store any logic.

Technically can be implemented building a component, use an open source one or simpy using DOM Events.

<img src="/images/microfrontends/event-bus.png" alt="event bus" title="Event Bus" width="480" height="320" />

<br>

## Microfrontend lifecycle

When we are working with components that are integrated within an application to work together, managing the "lifecycle" is very important. When I talk about "lifecycle" I mean the different phases through which a Microfrontend passes, from the Microfrontend is requested to the Microfrontend Registry Server to the Microfrontend is completely instatiated and running within the application.

I'm not going to set an standard lifecyle because I think this has to be customized depending on the company but I think at least two phases are necessary: loaded and ready. This phases are notified to the main application (and the rest component connected to the event bus) by events.

<br>

#### Loaded event

When a Microfrontend is requested to the Microfrontend Registry, the main file of the Microfrontend is delivered to the application. In this moment, 

- the Microfrontend main file (usually a Javascript file) is loaded within the main application (1), 
- an id is assigned by the Microfrontend Loader Component in order to identify a unique instance of the Microfrontend (2)
- Microfrontend attributes are initialized (3)
- A "microfrontend loaded event" containing information about the Microfrontend is fired to the Event Bus (4)

![loaded event](/images/microfrontends/loaded_event.png)

The id assigned to the Microfrontend is very important because it will be used to determine which instance of a Microfrontend is working in every moment. 

Scenarios in which more than one instance of a Microfrontend could be possible. Imagine for instance that a Microfrontend containing information about a product is available and it's necessary to implement a feature consisting on compare two products. The application could load two instances of the same Microfrontend and passing different products ids to each one. 

<br>

#### Ready event

Once the Microfrontend is loaded, 

- the main file of the Microfrontend will begin to request other files (language files, config files, assets, etc) to the Registry Server (1)
- some calls to the API could be made in order to get the data necessary to work (2)
- the Microfrontend is ready and throws a "ready event" containing its ID (3)
- the "ready event" is catched by the Loader and checks the ID contained in the "ready event" (4)
- the Loader makes the microfrontend instance visible (5)

![ready event](/images/microfrontends/ready_event.png)

<br>

#### Health check

When the application is composed by independent (business) components, sometimes some component could fail or not work as expected. In these scenarios, it's so useful not showing those components if they aren't work well. This capability can be implemented managing status events (loaded, ready) so that, initially the Microfrontends will be hidden until the ready events associated to them are catched. 

Once the Microfrontend Loader has received the main file of the Microfrontend and it has generated an ID for this Microfrontend, it waits for a ready event fired by this Microfrontend (containing the ID generated). When this event is received, the Microfrontend Loader shows the Microfrontend. 

If the Microfrontend can not fire the ready event (1) for some reason (error getting initial data for instance) or the event isn't received in a configured number of seconds (1), the Microfrontend Loader could show a default component (2), another Microfrontend or do nothing visible for the user and log the error to the backend layer in order to be analyzed

![healthcheck](/images/microfrontends/healthcheck.png)

By this way, the user doesn't realize that something could be wrong. For instance, think about in sites like Amazon where some components don't appear sometimes but you don't perceive that anthing isn't working well.

<br>

## Microfrontends Development Lifecyle 

Setting an archytectural style where pieces are distributed and the main principle is autonomy through the whole process (from the idea to the operation in production) requires a development lifecyle designed also around this principle. In this post I'm going to define a simple development lifecycle but it's could be more complete and complex.

Working with Microfrontends is not different as working with backend services. First and the most important part is to design the microfrontend from a business point of view, setting its functionality and contract. Then, the Microfrontend will be developed and tested. Finally, the microfrontend needs to be deployed and published in a "Microfrontends  Server" or "Microfrontends Registry" to be consumed.

![Dev Lifecycle](/images/microfrontends/dev_lifecycle.png)

<br>

## Definition

This is the first phase and, in my opinion, it's the most important because the microfrontend is a product that has to be defined from a business point of view. We have to keep in mind that a microfrontend isn't just an UI or visual components, so we need to have an end-to-end vision. 

The objetive is to define **WHAT** is necessary and **WHY** a new Microfrontend has to be created in order to solve that need. Questions like these are made in this phase in order to define our product:

- Why do we need a new microfrontend and what is the business need it resolves? There could be many reasons: many changes over the business capability, different technology needed, reusability between applications,...,etc
- There is other microfrontend or component in any existing application to resolve the business need? I prefer "monolith-first approach" (modularized and well designed). Then, if a microfrontend is needed to cover some functionality implemented in the monolith, refactoring to a microfrontend shouldn't be so complex.
- Which is the domain or subdomain that the microfrontend would belong to? We are building business pieces so it's very important set the microfrontend into a concrete domain.
- Who is going to be the owner? The owner will be responsible for the microfrontend along all its life.

<br>

## Desing

Once we know WHY and WHAT, the objetive is to define **HOW** is going to be built the Microfrontend in order to solve the business need.then we have to answer other questions (almost technical) like:

- Functional Design

  - What is the use case or feature performed?
- Which channels is it going to be consumed in?
  - How is it going to be tested?
- Which events is it going to listen to and fire?
  - Which visual properties are going to be customizables?
- ...
  

  
- Technical Design

  - Which parts does the Microfrontend need to solve the business problem?
- Which framework or technology is the best suitable for the different parts (UI, BFF, ..., etc)?
  - How does data has to be managed? How many services does it to manage?

  - Which services need to be consumed? All the services belong to the same domain or it's going to be necessary to consume services from several domains? 
- How does security capabilities are implemented (or should be)?
  - ...



<br>

## Build

Building a Microfrontend is similar to develop a little application. Depending on the complexity of the Microfrontend may be necessary to include several views and routes, several API calls, loading language files in order to manage several languages,...,etc. Maybe, a backend for frontend will be necessary.

<br>

## Test

Remember that Microfrontends are independent pieces that perform a business feature from a end-to-end perspective. So, end-to-end tests are mandatory and fundamental in this kind of architecture. Automatization of this tests is a key factor talking about Microfrontends.

We have to keep in mind that usually a Microfrontend is composed of a Frontend part and a Backend For Frontend part. Within the Frontend part, we have to remember that a Microfrontend

- Receives some parameters (html attributes), 
- Listens to some events and react to them
- Throws some events responding to some actions
- Declares some visual properties to be customized

so tests cases should be defined to cover every scenario (firing events, receiven events, visual customizations, etc...). I recommend you to define a good users stories showing how the Microfrontend should be worked. That means that before coding, you should know why you need a new Microfrontend but you should also know how that Microfrontend has to be tested.



## Deploy & Publish

Microfrontends need to be packaged and registered (deployed) in a "Microfrontend Registry Server" in order to be discovered by consumers, similar to "Register & Discovery" capabilities of a Microservices environment. 

The main part of a microfrontend is the UI that it'll be loaded for the consumers. The UI package should contain:

- **main file**: this file will be loaded by the consumer in order to run the microfrontend. When this file is loaded, it begins to request on demand the rest of files of the microfrontend (assets, config files, language files,...,etc) and API calls. It's similar a SPA application. This main file usually is a Javascript file.
- **other files**: these files are requested on demand when the microfrontend is running. For instance:
  - media files
  - language files
  - config files

This package (can be a zip file) will be "deployed" in the "Microfrontend Registry Server".

**If the microfrontend has a backend part like a backend for frontend, it has to be treat as a whole, versioning, deploying and publishing everything at the same time. **

<br><br>

# Microfrontends is a company decission



## Culture

Sorry, **Culture is a key factor for success** when you work with architectures "micro-x". Applying some architectural patterns is not possible if the company isn't ready. This is it. 

Cultural changes are necessary in order to get success. If you don’t transform your culture, you’re not going to success with “Microfrontends” or "Microservices". Culture is the more powerful strenght in your company.

![culture](/images/microfrontends/culture.png)

I'm not goint to talk about [Conway's law](https://en.wikipedia.org/wiki/Conway%27s_law) in this post but I do would like to remember this phrase from [Microsoft CEO Satya Nadella](https://news.microsoft.com/en-gb/2018/11/07/microsoft-ceo-satya-nadella-on-fuelling-tech-intensity-in-the-uk/) saying "every company is a software company". Nowdays, business means "digital business" and that is totally related to building software and delivering value faster than the competitors. 

If people from business departments are not involved in adopting this architectural style, you are going to fail working with this architectural style because only are going to add complexity to the system. Microfrontends will appears everywhere and the governance will be impossible.

A Microfrontend is (should be) like an usual business service defined from the business point of view:

- Resolves a business need
- Changes in functionality must be always origined by business changes

So, aspects like the following ones are fundamental in this kind of architectures (and in software development in general):

- No silos. Global vision
- Agile principles in software development
- Business people integrated into teams
- Ownership
- Autonomy over control

The way you build your software should be the way more suitable for your company and its characteristics: size, history, employees, maturity,...,etc.

<br>

## Where's the limit?

As I said previously, one of the main principles is to provide (visual) fully functional independent components that manage API calls and backend services. 

A Microfrontend is a product that is offered to a consumer, external or internal. The user of the microfrontend doesn't care about API calls or which backend services the microfrontend uses. 

The owner of the microfrontend is responsible for keeping this "business piece" up and running so, the ideal situation would be the one in wich the owner is responsible for all the elements, from UI part till the backend for frontend or the deepest service and all of those components are managed by the same team

Depending of how the company is organized it may be more feasible or not. Therefore, once again, adopting an architectural style implies organization and cultural changes to be successful. 

Microfrontends' style is not dividing frontend applications into pieces and managing backend calls within them. Microfrontends' style is to provide ownership and autonomy throughout full business functionalities. 

<br>

## It's not black or white. Be flexible and evolvable 

When we think about architectures, many times we think about a green field and the ideal architecture but we have to keep in mind that, at least you are a startup, these architectures have to live with other older architectures because business can't stop. 

Having this in mind, I would like to summarize the frontend states in three:

![why_microfrontends](/images/microfrontends/microfrontends-stages.png)

- **"Just Applications"**: there is no UI components. There are just applications consuming backend services. Business features are re-implemented in each application. Maybe, a components catalog could exist.
- **"Pseudo Microfrontends"**: there are UI components with a business sense, not just visual components. These components access to backend services to perform business actions and even could be owned and managed by independent teams, but they all deployed and published by libraries (NPM or similar) and the consumer applications integrate them in build-time. So, an integration phase (maybe complex) is realized in order to build and package the final applications. A change in a component implies rebuild and repackage the affected applications. Problems related to responsive or not, channels (mobile, web,...,etc) should be alredy being managed in this stage
- **Microfrontends**: it's an evolution of the previous stage. In this stage, UI business components are deployed and published independently, in a "Microfrontend (registry) server" that serves them to the parent applications in runtime. There is no complex integration phase. Parent applications and Microfrontends manage a contract in order to know how to use them. Like a service, if a Microfrontend changes and the contract is the same, the parent application doesn't need to be redeployed becase the new version of the Microfrontend will be loaded when the parent application is reloaded in the user browser.

Does it mean that you should build everything like a Microfrontend? I don't think so. 

In my opinion, you should take a global picture of your company and how its business is. Apply Domain Driven Design techniques in order to model complex domains. Once you know well your business and your company, think about where it's worth to build a Microntend because pros are better than cons, where it's worth to build "just an UI component" and where it's worth to build "just an application". It's not black or white. 

I prefer the **"monolith first" strategy** but always designing and building software thinking in business components that eventually could be extract to a NPM package or a Microfrontend (called by Http request) if a business need requires it.

If there are several applications that don't share any business feature, are very stables and their maintenance is "easy", why are you going to build Microfrontends or "business UI components" from the beginning? You are going to add complexity to those applications and you are not going to get any benefit from appliying those strategies. Build good monoliths apps, well structured in modules and components, with a good testing strategy and, if in the future you need to extract some components in order to be reused by other application, it'll be easy to extract them.

If you apply this strategy, the worst scenary could be that the technology used to build your applications doesn't allows to expose components as nom packages, web components or similar in order to be distributed or consumed by an HTTP request. But, if you have built a well designed applications and well tested, you will be able to build a new component in a different technology in order to be able to distribute those components requiered by others applications.

<br>

## A silver bullet? 

Microfrontends is an architectural style that try to resolve concrete problems. Maybe you have these problems in your entire company or only in certain areas. The key is to adopt this style when it was necessary because more complexity is being added to the system, more pieces and components that have to be managed.

For instance, Microfrontends may help you if:

- There are several business parts with different maintenance requirements than others. 
- Building fast prototypes of new features is requiered by Business but the current technology and processes difficult it
- The frontend team is very huge and compact and it would be better to distribute it in smaller teams around business capabilities
- Frontend applications are complex and big
- Applying a different technology (or framework) than the main one to build some functionalities is necessary 
- Your company is used to work in autonomous teams around domains and subdomains



<br>

<br>

I hope you’ve liked this post. I've tried to explain how I understand the term Microfrontends. In next posts, I'll show a little practical example implementing Microfrontends
