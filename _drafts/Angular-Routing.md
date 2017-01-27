---
author: jaruizes
layout: post
title: "Angular: Routing Basics"
date: 2017-01-23 00:30
category : Angular
comments: false
tags:
 - Angular 2
 - Javascript
---

In this post I would like to talk about the routing in Angular 2. The idea is to write several posts about this topic, from the basic aspects to the advanced ones.

### Introduction

If you are new in this type of frameworks "SPA oriented" you have to keep in mind that a navigation action doesn't have to be a request to the server. Actually, it isn't. In a SPA, the main page (named as shell) is loaded from the server but then, depending on the calls to the API or the user action, some sections or pages will shown or hidden without server interaction. 

In a non SPA application (like a JSP application), the navigation is performed by sending a request to the server in order that this one responds with the HTML that the new page has to have. This produces a complete reload of the application in the browser.

Frameworks like Angular need something to perform this kind of navigation in the client side without sending a navigation action to the server. It's important that each navigation produces a change in the URL because, for instance, maybe the user want to add it to his bookmarks.

The first step is to define the navigation map of the application/module. In this map, we can specify the different paths or routes that our application or module is going to have, the conditions or action necessary to navigate to this paths. While the user is navigating, the application can send some request to the server just in order to get the data necessary for the view. For instance, we define this navigation map:

> Pages: 
> * Home = / 
> * Feature1 = /feature1 
> * Feature2 = /feature2
> * Feature3 = /feature3
>     * Feature31 = feature3/feature31
>     * Feature32 = feature3/feature32
>     * Feature33 = feature3/feature33



In Angular this map is translated to this code (we are to get more detail later on):


```typescript
...
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'feature1', component: Feature1Component },
  { path: 'feature2', component: Feature2Component },
  { path: 'feature3', component: Feature3Component,
    children: [
      { path: 'feature31', component: Feature31Component},
      { path: 'feature32', component: Feature32Component},
      { path: 'feature33', component: Feature33Component}
    ]
  }
];
...
```

The Route object is in charge of "listening" the target URL to show the specified view (in Angular, each view is associated to a component).  


### Basic Navigation
After the introduction we're going to implement a basic navigation from the example above. You can download the complete code of this section executing this command:

```textmate
   git clone -b basic-navigation https://github.com/jaruizes/angular2-routing.git
```
<br>

##### Select a location strategy
We have to keep in mind that we want our application to navigate to several pages/views without a server call, modifying the URL and managing browser's history. 

If our browser support HTML5, the Route object will use **_pushState()_** and **_replaceState()_** methods to manage the browser's history object and perform the navigation. This methods don't execute any server call.

If our browser doesn't support HTML5, every change in the URL will produce a server call if the target URL doesn't contain "#". So, in this kind of browsers (old browsers), it's necessary to build the application URLs using the character "#". 

The Angular Route object covers these two kinds of navigation:


   1. PathLocationStrategy: this the default, using HTML5 pushState and replaceState.
   2. HashLocationStrategy: this is the strategy for old browsers, using the hash character (#) in the URL.



##### How do we configure the location strategy in Angular?

The location strategy is configured by a provider. We have to add the [LocationStrategy](https://angular.io/docs/ts/latest/api/common/index/LocationStrategy-class.html) and configure it to use the right class according to the strategy that we've chosen. Angular offers two class that extend the LocationStrategy class. These class are:

* [LocationStrategy](https://angular.io/docs/ts/latest/api/common/index/PathLocationStrategy-class.html)
* [HashLocationStrategy](https://angular.io/docs/ts/latest/api/common/index/HashLocationStrategy-class.html)


So to configure our app to use a strategy we have to add a provider and specify the class that implements the strategy. In this case, we add it in _app.module.ts_ file:

```typescript
...

providers: [{provide: LocationStrategy, useClass: HashLocationStrategy}]

...
```

We are going to select **HashLocationStrategy** to start the example and then, we'll change the strategy and we'll see the impact. The strategy by default is PathLocationStrategy. If we are going to use this strategy we don't have to anything to configure it


##### Static navigation

Once we've configured the location strategy we are going to configure de navigation map. To do this, we create a new file called _app.routing.ts_ where we define the navigation map:


```typescript
import { Routes, RouterModule } from '@angular/router';
import {Feature1Component} from "./feature1/feature1.component";
import {Feature2Component} from "./feature2/feature2.component";
import {Feature3Component} from "./feature3/feature3.component";
import {HomeComponent} from "./home/home.component";
import {Feature31Component} from "./feature3/feature3-1/feature31.component";
import {Feature32Component} from "./feature3/feature3-2/feature32.component";
import {Feature33Component} from "./feature3/feature3-3/feature33.component";

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'feature1', component: Feature1Component},
  { path: 'feature2', component: Feature2Component},
  { path: 'feature3', component: Feature3Component,
    children: [
      { path: 'feature31', component: Feature31Component},
      { path: 'feature32', component: Feature32Component},
      { path: 'feature33/:origin', component: Feature33Component}
    ]
  }
];

export const routing = RouterModule.forRoot(routes);
```

Each route is associated with a Component that manage this path. Later we'll see how we can show several components in a single path using routes.  
Once we have the navigation map, we are ready to implement the navigation actions.

The easy way consist on a simple <a> tag with the [routerLink directive](https://angular.io/docs/ts/latest/api/router/index/RouterLink-directive.html) associated.
For instance, we add a navigation bar in the main page of our application:

```typescript
<nav style="border: 2px solid black; padding: 1rem; background-color: lightgrey">
  <a routerLink="['/']">Home</a>
  <a routerLink="['/feature1']">Feature1</a>
  <a routerLink="['/feature2']">Feature2</a>
  <a routerLink="['/feature3']">Feature3</a>
</nav>
```

##### Dynamic navigation
In the real world we have to perform navigation actions depending on business logic and these cases are so dynamic so we can not use just anchor tags.
A easey way to do this is using the method _navigate_ of [Router class](https://angular.io/docs/ts/latest/api/router/index/Router-class.html#!#navigate-anchor).
Programatically we select the target path and it allows to pass some params or for instance, take a relative or absolute path. 

This is an example:

```typescript
...
export class Feature32Component {
   ...
   ...
   moreDetail() {
       // Simple navigation
       this._router.navigate(['/feature3/feature33']);
   }
   ...
   ...
}
...
```
You can check the official documentation to know more detail of the params of the [navigate method](https://angular.io/docs/ts/latest/api/router/index/Router-class.html#!#navigate-anchor).