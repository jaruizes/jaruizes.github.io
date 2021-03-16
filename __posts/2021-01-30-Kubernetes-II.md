---
author: jaruizes
layout: post
title: "Kubernetes - The JARC way (II)"
date: 2021-01-31 01:30
category : Kubernetes
comments: false
imagefeature: k8s/k8s-objects.png
tags:
    - microservices
    - kubernetes
---

# Kubernetes "The JARC way" (II)
This is the second post of the serie Kubernetes "The JARC way". 

The main objetives for this pod is to deploy (manually) a simple application to a local cluster showing aspects like:

- How to deploy an application with different parts
- How to inject configs and secrets
- How to manage persistent information

<br/>

# Use case

The use case is the following:

- We have three services in different domains: 

  - Orders Service
  - Payment Service
  - Notification Service

  <br>

- The order of execution is:

  1. User calls to Order Service in order to create an order
  2. Order Service calls to Payment Service
  3. If everything is OK, Order Service calls to Notification Service
  4. User calls to Order Service in order to list his orders

  <br>

- The only service that can be invoked from outside the cluster is Orders Service.

The source code is available here (TODO: insert github url)

<br/>



# Deploying services

We're going to see how we can deploy those three services to Kubernetes cluster. The first way in wich we'll do it will be using just Pod descriptors (YAML file). Later, in this series of post, we'll use Deployment objects. 





<br />

This is the first post on "Kubernetes - The JARC way". In the next posts, we'll see in detail the most important Kubernetes objects associated to development aspects instead of learning each one without more context....