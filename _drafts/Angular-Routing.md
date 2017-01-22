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

If you are new in this type of frameworks "SPA oriented" you have to keep in mind that a navigation action doesn't have to be a request to the server. Actually, it isn't. In a SPA, the main page (named as shell) is loaded from the server but then, depending on the calls to the API or the user action, some sections or pages will shown or hidden without server interaction. 

This is the main difference with the JSPs approach, for instance. In a non SPA application, the navigation is performed by sending a request to the server in order that this one responds with the HTML that the new page has to have. This produces a complete reload of the application in the browser.

So, to do that, frameworks like Angular need something to perform this kind of navigation in the client side. It's important that each navigation produces a change in the URL because, for instance, maybe the user want to add it to his bookmarks.

The first step usually is to define the navigation map of the application or module. In this map, we can specify the different paths or routes that our application or module is going to do, the conditions or action necessary to navigate to this paths.
 
 