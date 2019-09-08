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

I would like to begin this post with the term "Microservices" in order to introduce "Microfrontends". Microservices are everywhere. Sometimes the experience is positive, sometimes is negative but the term is in the air. It is usually related to backend architecture but talking about how a system could be decomposed in autonomous and independent pieces, owned and developed by single teams, deployed independently and working all together.

Why most of the companies are only focusing on backend? When we are developing a product or features, we shouldn't forget that the most of features contains backend and frontend parts. If we really want to deliver value to the customers, we should deliver end-to-end features within a team. Just applying an architectural style to our backend (based on microservices or not) or organized in teams with no end-end skills, we won't get enough autonomy to deliver (and maintain) end-to-end features:

![Sam Newman Tweet](/images/microfrontends/newman.png)

It seems logical that the next step should be build end-to-end functionalities. In this context, the term **Microfrontend** really begins to make sense

# Building products not just "services"

Usually when we talk about a software products we are talking about something with an user interface with which an end user interacts to perform some business actions. For instance, when we access to a banking application we want to see our global balance, last movements of some account or make a transfer. We only interact with the user interface but we expect to make actions and receive a result. We doesn't care if the application calls to an API or if our data is showing there magically. We want to application works well, just that.

As software developers, we know that behind the UI there are services, data and other systems working together in order to provide business capabilities to the end users. Everything working together is what is providing value to the end user because:

- If the UI is great but backend services don't work well (or not exist) the UI will not provide value to the user. 
- If backend services work well but there is no UI or the UI doesn't work, the system will not provide value to the user. If several applications have similar business need (features) and the UI looks different in each one or works differently (because UI or services), the user experience is so bad

![why_microfrontends](/images/microfrontends/products.png)

So, if we want to provide business value to end users we will need a good user interface working with good services like a whole. 

---

And, many times using the same UI accross applications is necessary because we'll keep the business functionality inmutable and we will also manage better the user experience: the same UIs will be used in internal applications so we'll detect bugs earlier and we'll suffer using those UIs.

Well, you can be thinking about APIs and products based on APIs. Your right. This could be a kind of product that a company provide to an other company in order to that company builds an UI over this APIs and provide applications to an end user or only to integrate those two companies. 

The product of the first company is the API but this API, in the most of cases, isn't going to be consumed directly by an end user, so an UI needs to be built becoming a product. The product is offered by the last company but it's an end-to-end product, so we're talking about the same: __providing end-to-end products__.  

---



## End-to-end perspective

Many companies have started to modernize their architectures in order to build better applications, more scalables and more evolvables. Some of theses companies use a Microservices style, others have decided to back to better monoliths and others are thinking about how improve the way to build software. In the most of them there is something common: they think about services, independent teams, agility, etc but focused on backend systems (APIs, backend services, migration HOST to (micro) services, etc...). 

But, something is true: the most of features are end-to-end, composing for elements in every layer:

![why_microfrontends](/images/microfrontends/focus_in_backend.png)

So, taking an approach focused in backend services or systems is not enough efficient:

- If you build wonderful (backend) services around business capabilities but you don't build an UI associated to those business capabilities your are not building unique or inmutable business capabilities. You are building differents flavours of the same business capability. 

  ![why_microfrontends](/images/microfrontends/feature-different-views.png)

  You are building **"headless business features"** and you have to develop "different heads" in order to provide these features to the final users. 

  For instance, in a banking environment, why do you have to develop the account movements view in the main consumer application and you also develop a similar view in the backoffice application or in another application also used by the customers? 

  

- If you achieve a great autonomy in backend systems but you don't do the same in the frontend apps, your (backend) autonomy is not real because you can not deliver end-to-end features to the end user without depending others. 

  ![why_microfrontends](/images/microfrontends/autonomy.png)

It seems that building end-to-end features would be more efficient, isn't it? 

![why_microfrontends](/images/microfrontends/end-to-end-features.png)

If one team is able to develop all the necessary elements for deliver a feature, 

- autonomy is great because the team doesn't depend on others
- the feature is owned by a team (functionally and technically)
- quality is applied end-to-end



## Keep the business features inmutables to the user and reuse them

Imagine this scenario. It's not the best approach to organize a company architecture but it could be something real in many companies:

![example](/images/microfrontends/situation-example.png)

We can see two applications: 

- Customers: application in which customers perform business actions. 

- Customer Care: application used by company employees to help to their customers. This application try to be similar to the Customers application in order to give a good service to the customer.

Both applications have their own backend for frontend in order to orchestrate calls to different services and manage details regarding to different channels. In some companys, a different frontend developments are built in each application. In others, the decission is to build a frontend module containing the functionality and this module is integrated in both applications. The backend for frontend usually depends on the application and it isn't reused and backend services are the same in both applications. 

If a backend service change and a new version is released, the backend for frontend will consume this new version of the service. So, business capabilities provided by backed services could be defined as inmutables.

If the implementations of similar business features between applications is not considered as a whole, they are **mutable**. That means they are differents implementations of the same business capability:

![example](/images/microfrontends/mutable-fetatures.png)

The ideal situation would be that the business feature was reused from the top layers to the bottom layers, but in some cases you are not responsible for all the elements (for instance external services). The target is to build end-to-end blocks of business capabilities to be reused. 

It we can isolate business capabilities in the frontend part (UI and Backend For Frontend), consuming instances of these business capabilities and releasing new versions when something changes, we are building inmutables business capabilities in the frontend layer:

![example](/images/microfrontends/inmutable-fetatures.png)



# Microfrontends: fully business components

As we saw in the previous section, if we could build independent and fully business components, composed of all the necessary elements, versionables, developed, owned and maintained by a team and **loaded and integrated at runtime in the application** we are building little products

![microfrontends-idea](/images/microfrontends/microfrontends-idea.png)



## What is a Microfrontend?

The target associated to this concept is to provide a "headfull" business service instead just a backend service ("headless"). So obviously, the main part of a microfrontend is the frontend part. This part is what will be consumed and loaded by applications or another microfrontends. 

To get fully business capabilities, calling to backend services will be necessary. How is it managed? Here, there are several possibilities:

- Building a backend piece (**backend for frontend**) in order to manage calls to business API, orchestration, information adaptation to the channel,...,etc. This piece will be also part of the microfrontend, sharing ownership. This approach will be the most usual because in real systems, orchestration of services is very common in the most functionalities.

- Access to a business service already implemented in the same domain or in different domains or event external. In this case, the microfrontend is the part that is exposed to the consumer (it's the product), so it has to guarantee everything works. The consumer doesn't care about which services are consumed by the views provided for the microfrontend. The consumer only sees the UI part. 

  If the services consumed by the microfrontend change, if it's necessary the microfrontend will have to be updated relasing a new version of the microfrontend. 

  If services are in the same domain or have the same owner it will be easier to keep the microfrontend updated than if the services are in other domains or they are external. 

So, in the most of cases a microfrontend will be composed by:

- An user interface implemented in any frontend technology

- A Backend for Frontend implemented in any technology that supports interaction with the UI component.

  

It's very important to consider all the components associated to the microfrontend as a whole. 



## Loaded and integrated at runtime (like services)

This is the key when we talk about independent and autonomy components. The devil is in the detail. Think about **Rest services** are consumed by the applications or another services:

- There is a contract where the endpoint information is declared: request, response, security if needed, etc...
- Consumers only send an HTTP call to an URL as the service contrat says and wait for a response. Consumers doen't know any detail about the internal implementation of the service or how the service manages its data. Languages/frameworks can be different between consumers and service.
- Consumers are deployed in a different server that the service artifact
- If the service needs to be updated by some reason (fix a bug for instance), the application doesn't need to be rebuilt and redeployed to get the changes.

Now, think about **modern frontend apps** are working:

- The application is coded in a specific language/framework, mainly javascript
- The application can be divided in components and components can be loaded on demand, at rutime, if the user navigates to the view using those components
- The application needs to be packaged with its components although they can be loaded at runtime (on demand) or all together when the application starts
- The components and the application are deployed in the same server, as a whole
- If a component needs to be updated by some reason (fix a bug for instance), the application needs to be rebuilt to package the new version of the component and redeployed. 

These models are similar but different because a REST service is totally decoupled to the client application and, both of them are independent in development, deployment and maintaining. 



### Web Components

You can be thinking about Web Components and Microfrontends. It's true that a microfrontend is loaded like a web component by the parent application, using it like other HTML tag. But, once again, the different is when the component is integrated in the parent application. Buid-time? Runtime?  

In the most of cases, the approach to use Web Components is mainly by NPM (or Bower) packages: 

- need to be declared in development time (package.json / bower.json), 
- need to be downloaded in development time
- need to be packaged and deployed with the application 

For instance, __[Webcomponents.org](https://www.webcomponents.org/introduction)__ and __[LitElement](https://lit-element.polymer-project.org/)__:

![why_microfrontends](/images/microfrontends/webcomponents-publish.png)

This approach isn't the ideal one because there is a "strong" coupling between the application and its components. 

> The target is being able to consume fully functional components like services without packaging them inside the application



## Stages

I'm going to summarize the stages to go to Microfrontends in three:

![why_microfrontends](/images/microfrontends/microfrontends-stages.png)

- **No Microfrontend**: there is no UI components. There are just applications

- **"Pseudo Microfrontends"**: there are UI components with a business sense. These components access to backend services to perform business actions and even could be owned and managed by independent teams, but they all deployed and published by libraries (NPM or similar) and the consumer applications integrate them in build-time. So, a complex integration phase is realized in order to build and package the final applications. A change in a component implies rebuild and repackage the affected applications. Problems related to responsive or not, channels (mobile, web,...,etc) should be alredy being managed in this stage

- **Microfrontends**: it's an evolution of the previous stage. In this stage, UI business components are deployed and published independently, in a "Microfrontend (registry) server" that serves them to the parent applications in runtime. There is no complex integration phase. Parent applications and Microfrontends manage a contract in order to know how to use them. Like a service, if a Microfrontend changes and the contract is the same, the parent application doesn't need to be redeployed becase the new version of the Microfrontend will be loaded when the parent application is reloaded in the user browser.

  

# Microfrontends: an architectural style

Microfrontends goes beyond frontend frameworks and their power fight: Angular vs React vs Vue vs ...

> Building microfrontends means adopting an **archytecture style**, building and delivering end-to-end business pieces, defined by a formal contract and with a clear ownership, packaged and deployed independently, to be integrated and consumed at runtime within a frontend application or even by other microfrontends.

Microfrontends are not about an specific implementation. Like some architecture styles, it's important to set:

- which **kind of problems or challenges could resolve** and when it's worth applying or not.
- which are the **main principles and patterns**

Fowler and Lewis wrote a post in 2014 talking about Microservices and what they mean. It was some years ago but I think it is a "master post" we always have to keep in mind. In this post, nine principles are set:

- Componentization via Services
- Organized around Business Capabilities
- Products not Projects
- Smart endpoints and dumb pipes
- Decentralized Governance
- Decentralized Data Management
- Infrastructure Automation
- Design for failure
- Evolutionary Design

Let's try to apply microservices principles to frontend world:

### Componentization via Services

We're used to build UI components, package them into libraries and publish them in the NPM (or bower) repository. This means that every application uses these components by importing them in build time, packaging all together. Although you are using lazy loading and components are loaded on demand, the application consist on a single package "deployed" in the same location. If a component changes, the whole application has to be rebuilt to get the changes and redeployed.

So, in this scenario, autonomy isn't the main characteristic…But, the idea behind "microfrontends" is just the opposite:

> __what if we'd build artifacts that encapsulate end-to-end features and we could consume them at runtime by http calls?__ The idea behind Micro frontends is building "headfull services", that means, delivering end-to-end features by components consumed in runtime by http calls.

Consuming frontends as services means that:

- Microfrontends encapsulate all the backend API calls they need, so they aren't just UI. They are end-to-end components
- Microfrontends expose contracts as services do, input and outputs, events and styles.
- Microfrontends are tested individually
- Microfrontends are deployed independently, so it's not necessary to rebult the parent application is something change in the microfrontend
- Microfrontends are developed and owned by a team



##### Tip for Java developers

If you use Maven, the most of the libraries are integrated in build-time and everything is packaged in the same artifact. If a dependency changes, rebuilt and repackage is necessary. 

The most of times, we extract some dependencies and package them to be deployed independently as a service and consumed by a simple HTTP call. Using Maven, you also find dependencies with "provided" scope. Dependencies tagged with this scope will not be packaged and will be provided by the execution environment (usually an application server). In both cases, the code of these services are inside the parent application anymore. 

This is similar to the target of Microfrontend: not packaging all the pieces within the parent application and being integrated and consumed at runtime



### Organized around Business Capabilities

Microfrontends aren't UI components (later we'll see the differences between them). Microfrontends means implementing end-to-end business features "as a service". Descomposing the system into business capabilities should be the first step if we want to adopt this architecural style.

We do this exercise when we're defining microservices associated to our system but we do not do the same from the UI point of view and we build the same views in many applications. 

It's also true that, in some companies, business capabilities are treated from the frontend but sometimes this exercise is done taking only one application.

In this point, the key is delivering a complete business feature to consumers instead of offering business APIs to the final applications implements the UI. Not confusing this with Open APIs.



### Products not Projects

Building Microfrontends means building products, not projects. A team builds and maintain one or more microfrontends of which is the owner. The team is responsible for the "UI Service" over its full lifecycle.

As the Microfrontend encapsulates backend API calls and the user of the Micro frontend only "receives" the UI Service, the team is also responsible to maintain these API calls updated and working. 

Besides that, several versions of a Microfrontend could be published and be consumed, so the team also has to keep in mind this aspect and managing the retirement of versions out-of-date.



### Smart endpoints and dumb pipes

Currently there are a lot of frameworks or products to build frontend applications and its business logic (ok, presentation logic). Communication between components within the application is supported by the framework choosen capabilities. 

In a Microfrontend style, components are designed and developed as decoupled as possible, so components has to be independent, loaded in runtime and communications between components couldn't be supported by a framework. 

Microfrontends communications must be supported by DOM standards: html tags, attributes and DOM events. It's possible to use some libraries to abstract the frontend event bus but this tool only has to be used to provide publish/sibscribe capabilities. Application logic never is in the event bus.



### Decentralized Governance

Similar to Microservices, a centralized governance implies a single technology o framework. Once a framework is choosen then libraries or some components are built to be delivered to development teams in order to get more productivity. When several applications have been developed, changing the framework becomes a big challenge.

Choosing just one technology or framework we could cause several problems like:

- Not using the best tool to solve a problem
- People gets bore because "it's always the same"
- Locking to a framework, components or even a way (the framework way) to develop.

> If we can load components in runtime by a http call and these components are used as the same way as other HTML components, why do I have to centralize the technology or frameworks?
>

So adopting Microfrontends is not adopting one framework or technology. It's adopting a way to build UI Services that can be consumed at runtime by any application, similar to backend services (http) are consumed.

Microfrontends associated to business features can be developed with the best technology or framework according to the complexity, requirements or business context. 

This doesn't mean that there is no Governance. Governace means principles, rules, patterns,...,etc not technical implementations. Normally, some "core actions" need to be defined to be implemented in every microfrontend. For instance, actions like language changing to suppont multilanguage sites: your company can set the principle that every Microfrontends should listen to an "language changed" event and reacting to it.

Similar with Security concerns. This needs to be defined globally and teams in charge of microfrontends must follow the patterns and rules.



### Decentralized Data Management

In Microservices, when we talk about this subject we mean how to manage data associated to each microservice:  which database or which model the service is going to use.

In Microfrontends, __data management means "backend API calls"__. How the microfrontend is going to get its data? Technically speaking you can be thinking about REST or GraphQL for instance, but the key isn't that, the key is getting autonomy end-to-end in order to deliver a complete business feature. 

Patterns like Backend For Frontends are really helpful in this target because if a microfrontend needs to manage data from several domains to solve some business feature, it's necessary a piece to encapsulate this logic. Or for instance, it could be necessary that the microfrontend shows different amount of information depending of the channel.

Maybe you are wondering about security and how the microfrontends get their data in a secure way. Microfrontends are loaded at runtime, dinamically, some of then in public areas and some of then in private areas. To access this private areas is neccessary that the user is authenticated. This is responsability of the main application, not of the microfrontends. 

Microfrontends need to know if the user is athenticated and how to get the tokens (or whatever you use) in order to invoke backend APIs. In this point, two strategies are possible:

- The main app intercepts all the backend calls and adds the security headers so microfrontends don't have to implement it
- Microfrontends are allowed to get the tokens received when the user is authenticated and they are responsible for generating the security headers they need to access to the backend services.



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



# UI Components vs Microfrontends (Business Components)

The most of companies have developed a set of UI components, from simple inputs to complex tables or elements. This components doesn't work by themselves because they don't call to the API to manage data. Instead, they need other components call to the API.

> Microfrontends means:
>
> - End-to-end business components
> - UI components, views and behaviours
> - Backend API calls
> - Logic or State



A Microfrontend is a piece of software that makes sense for the end user by itself**. If the final user access to the Microfrontend directly, the final user gets value from that Microfrontend and he could do a business operation. For instance: 

- Microfrontend - Account Detail: UI views and backend for frontend making the necessary API calls for getting the account info
- Microfrontend - Products Catalog: UI views and backend API calls for showing the products catalog
- Microfrontend - Customer Profile: UI views and backend API calls for managing customer profile

An UI Component, doesn't have sense by itself to the end user because it doesn't manage backend services. 

As I said in the previous section, Microfrontends require to be loaded at runtime and not being packaging inside the application. Usually, the components catalog is published in NPM and it's declared in the application is going to use them. 

If the components are Web Components they can be imported in any application independently of how it's built. This is OK for Microfrontends because we'll see later a principle of Microfrontends Architecture about different technology choices. But, if the components are built with an specific framework to be imported in applications built with the same framework there is a limitation about setting a Microfrontends Architecture because a "vendor coupling" is declared

UI Components could be part of the visual layer of a microfrontend. Within a microfrontend, those UI Components plus backend components acquire real business capabilities to the final user:

![microfrontend-vs-uicomponents](/images/microfrontends/microfrontend-vs-uicomponents.png)

# Visual concerns 

When you listen the term "microfrontend" for the first time you wonder:

- Responsive? Is this responsive? Mobile first?
- Are they "static"? If do we need to change some visual properties depending on the "parent application"?

Well, **those questions are not about microfrontends. They are about UI components.**

Think about your UI catalog components and its complex components. They are designed thinking about responsive concerns or if they are going to be used in mobile applications or not. Does your company have UI components designed for mobile applications? If it does, you could build microfrontends over them

> A Microfrontend could have several views depending of the channel it was instantiated. The restriction is all those views belong to the same logical piece, are owned by the same owner (business and technical) and provide the same business functionality in order to be reused in another applications.

Microfrontends don't have to be static and closed pieces from a visual point of view. They could declare some properties in order to customize their aspect or appliying themes. Custom CSS properties are very helpful to achieve this capability.



# Microfrontend contract

If we want to treat Microfrontends as services we need to define a contract to be used by the customers to work with them. What should a Microfrontend define?

![contract](/images/microfrontends/contract.png)

- Basic data / metadata: name, description, owner, area
- Attributes: input parameters to be set when the microfrontend is used
- Custom visual properties: which visual variables could be modified
- Events: 
  - Which events is listening to
  - Which events is firing and when



# Microfrontends Development 

Working with Microfrontends is not different as working with backend services. First and the most important part is to design the microfrontend from a business point of view, setting its functionality and contract. Then, the Microfrontend will be developed and tested. Finally, the microfrontend needs to be deployed and published in a "Microfrontends  Server" or "Microfrontends Registry" to be consumed.

## Product Desing

This is the first phase and it's the most important because the microfrontend is a product that has to be defined from a business point of view. We have to keep in mind that a microfrontend isn't just an UI or visual components, so we need to have an end-to-end vision. 

We'll have to answer questions like these in order to define our product:

- Why do we need a new microfrontend and what is the business need it resolves? There could be many reasons: many changes over the business capability, different technology needed, reusability between applications,...,etc
- There is other microfrontend or component in any existing application to resolve the business need? I prefer "monolith-first approach" (modularized and well designed). Then, if a microfrontend is needed to cover some functionality implemented in the monolith, refactoring to a microfrontend shouldn't be so complex.
- Which is the domain or subdomain that the microfrontend would belong to? We are building business pieces so it's very important set the microfrontend into a concrete domain.
- Who is going to be the owner? The owner will be responsible for the microfrontend along all its life. 

Once these questions are resolved, then we have to answer other questions (almost technical) like:

- UI Design

  - Which channels is it going to be consumed in?

  - Which events is it going to listen to and fire?

  - Which visual properties are going to be customizables?

  - Which framework or technology is the best suitable?

    

- Backend Services

  - How does data has to be managed? How many services does it to manage?
  - Which services need to be consumed? All the services belong to the same domain or it's going to be necessary to consume services from several domains? 
  - How does security capabilities are implemented (or should be)?



## Build

Once requirements are set, building a Microfrontend is similar to develop a little application. Depending on the complexity of the Microfrontend may be necessary to include several views and routes, several API calls, loading language files in order to manage several languages,...,etc. Maybe, a backend for frontend will be necessary.

Developers work the same way as the work when they are developing an application: code, test and review. Remember that Microfrontends are independent pieces that 

- receive some parameters (html attributes), 
- listen to some events and react to them
- throw some events responding to some actions
- declare some visual properties to be customized

so they have to be tested end-to-end before releasing it: the frontend part, the backend part and everything together. 



## Publish

Microfrontends are like services and they need to be packaged and registered (deployed) in a "Microfrontend Registry Server" in order to be discovered by consumers, similar to "Register & Discovery" capabilities of a Microservices environment. 

The main part of a microfrontend is the UI that it'll be loaded for the consumers. The UI package should contain:

- **main file**: this file will be loaded by the consumer in order to run the microfrontend. When this file is loaded, it begins to request on demand the rest of files of the microfrontend (assets, config files, language files,...,etc) and API calls. It's similar a SPA application. This main file usually is a Javascript file.
- **other files**: these files are requested on demand when the microfrontend is running. For instance:
  - media files
  - language files
  - config files

This package (can be a zip file) will be "deployed" in the "Microfrontend Registry Server".

**If the microfrontend has a backend part like a backend for frontend, it has to be treat as a whole, versioning, deploying and publishing everything at the same time. **



# Microfrontends is a company decission

## Domain Driven Design

Microfrontends are technical representation of a business subdomain and they birth because a business need. Within a domain or subdomain we'll find Backend Services but we'll also find "visual services" or Microfrontends. Both of them provide business capabilities and because of that, a business owner is required. 

If people from business departments are not involved in adopting this architectural style, you are going to fail working with this architectural style because only are going to add complexity to the system. Microfrontends will appears everywhere and the governance will be impossible.

A Microfrontend is (should be) like an usual business service defined from the business point of view:

- Resolves a business need
- Changes in functionality must be always origined by business changes



## Backend: Where's the limit?

As I said previously, one of the main principles is to provide (visual) fully functional independent components that manage API calls and backend services. 

A microfrontend is a product that is offered to a consumer. The user of the microfrontend doesn't care about API calls or backend services that the microfrontend performs. The owner of the microfrontend is responsible for keeping the "business piece" up and running so, the ideal situation would be one in wich the owner is responsible for all the elements, from UI part till the backend for frontend or the deepest service and all of those components are managed by the same team

Depending of how the company is organized it may be more feasible or not. Therefore, once again, adopting an architectural style implies organization and cultural changes to be successful. 

Microfrontends' style is not dividing frontend applications into pieces and managing backend calls within them. Microfrontends' style is to provide ownership and autonomy throughout full business functionalities. 



## A silver bullet? 

As I mentioned before, Microfrontends is an architectural style that try to resolve concrete problems. Maybe you have these problems in your entire company or only in certain areas. The key is to adopt this style when it was necessary because more complexity is being added to the system, more pieces and components that have to be managed.

For instance, Microfrontends may help you if:

- There are several business parts with different maintenance requirements than others. 
- Building fast prototypes of new features is requiered by Business but the current technology and processes difficult it
- The frontend team is very huge and compact and it would be better to distribute it in smaller teams around business capabilities
- Frontend applications are complex and big
- Applying a different technology (or framework) than the main one to build some functionalities is necessary 
- Your company is used to work in autonomous teams around domains and subdomains



