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

