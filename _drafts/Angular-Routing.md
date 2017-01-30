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
&nbsp;

For instance, in Angular, this map is translated to this code (we are to get more detail later on):


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
&nbsp;
### Navigation Service
Angular doesn't provide a navigation service in its core. The navigation service is an additional module that it's necessary to import in our project.

```typescript
import { RouterModule, Routes } from '@angular/router';
```
&nbsp;

So, we are importing two elements:

* [Routes](https://angular.io/docs/ts/latest/api/router/index/Routes-type-alias.html): This is a Type representing an array of elements "Route". Route is an interface that declares all the properties that a route can have. Later, in this and in future posts, we will see this properties and theirs uses.   
* [RouterModule](https://angular.io/docs/ts/latest/api/router/index/RouterModule-class.html): adds directives and providers.   


Basically, the Route object is in charge of "listening" the target URL to show the specified view (in Angular, each view is associated to a component).  


### Basic Navigation
After the introduction we're going to implement a basic navigation from the example above. You can download the complete code of this section by executing this command:

```textmate
   git clone -b basic-navigation https://github.com/jaruizes/angular2-routing.git
```
<br>

##### Selecting a location strategy
We have to keep in mind that we want our application to navigate to several pages/views without a server call, modifying the URL and managing browser's history. 

If our browser supports HTML5, the Route object will use the methods **_pushState()_** and **_replaceState()_** to manage the browser's history object and perform the navigation. This methods don't execute any server call.

If our browser doesn't support HTML5, every change in the URL will produce a server call if the target URL doesn't contain "#". So, in this kind of browsers (old browsers), it's necessary to build the application URLs using the character "#". 

The Angular Route object covers these two kinds of navigation strategies:

1. PathLocationStrategy: this the default, using HTML5 pushState and replaceState.  
2. HashLocationStrategy: this is the strategy for old browsers, using the hash character (#) in the URL.  
&nbsp;

##### How do we configure the location strategy in Angular?

The location strategy is configured by a provider. We have to add the [LocationStrategy](https://angular.io/docs/ts/latest/api/common/index/LocationStrategy-class.html) and configure it to use the right class according to the strategy that we've chosen. Angular offers two class that extend the LocationStrategy class:

  * [PathLocationStrategy](https://angular.io/docs/ts/latest/api/common/index/PathLocationStrategy-class.html)
  * [HashLocationStrategy](https://angular.io/docs/ts/latest/api/common/index/HashLocationStrategy-class.html)

These ones are not part of Angular core. They are located in the  [Common module]()https://github.com/angular/angular/tree/master/modules/@angular/common). 
So to configure our app to use a strategy, we have to add a provider and specify the class that implements the strategy. In this case, we add it in _app.module.ts_ file:

```typescript
...

providers: [{provide: LocationStrategy, useClass: HashLocationStrategy}]

...
```

We are going to select **HashLocationStrategy** to start the example and then, we'll change the strategy and we'll see the impact. The strategy by default is PathLocationStrategy. If we are going to use this strategy we don't have to anything to configure it


##### Static navigation

Once we've configured the location strategy we are going to configure de navigation map. To do this, we create a new file called _app.routing.ts_ where we define the navigation map:


```typescript
import {Routes, RouterModule} from '@angular/router';
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
&nbsp;
##### Dynamic Navigation

In the real world, we usually have to perform navigation actions depending on business logic and we can not use just anchor tags.
A easy way to do this is using the method _navigate_ of [Router class](https://angular.io/docs/ts/latest/api/router/index/Router-class.html#!#navigate-anchor).
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


##### What about params?

We've seen how to navigate but many times passing some params is necessary. In Angular, we need to declare the params that the target path expects. 
The way to declare them is by using "/:param". For instance:

```typescript
{ path: 'feature33/:origin', component: Feature33Component}
```

And the ways to navigate passing params are the followings:

* Static navigation
```typescript
...
<a [routerLink]="['./feature33', 'feature3']">Feature 3-3</a>
...
```

* Dynamic navigation
```typescript
...
goDirectlyTo33() {
    this._router.navigate(['/feature3/feature33','feature1']);
}
...
```
&nbsp;  
 
### Putting all together
Once we've configured the routes and defined the navigation actions, we can execute the whole application to check how the navigation is working. You can find the code in [github](https://github.com/angular/angular/tree/master/modules/@angular/router).

To launch the project you have to execute this command:

```textmate
   ng serve
```

(you need to have installed (angular-cli)[https://cli.angular.io/]).

Angular will build and package the application but it'll not open our browser...so you have to open the browser and write the following URL: _http://localhost:4200_

The first view of the application is the following:

![Home](/images/routing-basics/screen_1.png)

As you can see in the address bar, the URL contains the symbol '#'. This is because we've choose the Hash Strategy. 

If we click on the "Feature 1" link, for instance, the application goes to this route and shows the template associated to the Feature1Component:

![Feature1](/images/routing-basics/screen_2.png)

This navigation has been the static one, by using the _routerLink directive_. In the current view you can see a HTML select with two options and also you can see a button for navigating directly to 3-3.

If you click on whatever button, you'll perform a dynamic navigation. For instance, we are going to click on the second button. The application will show the template associated to Feature33Component:

![Feature33](/images/routing-basics/screen_3.png)