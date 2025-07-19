---
title: Domain Driven Design + Design Thinking
tags: [domain driven design, design thinking, cloud-native]
style: fill
color: info
description: Highlighting a neat discovery online that uses Design Thinking in their approach to Domain Driven Design
---

# Design Thinking + Domain Driven Design (DDD): An innovative approach to building scalable systems

Slightly outside GIS interests, there is an innovative group on Github that uses a "Design Thinking" (UX) approach to DDD microservices: a complex but worthwhile approach to building enterprise level information systems (and keep your sanity).

- https://github.com/ddd-crew/ddd-starter-modelling-process

## What is Design Thinking?

Design Thinking refers to a set of User Experience (UX) worksheets (called "canvases") to help you progressively clarify your business/research ideas. Check out this link for more: 

- https://www.interaction-design.org/literature/topics/design-thinking

## What are Microservices?

Microservices are a way of chunking up your business functionality into smaller, more manageable services. The beauty of this approach is that they don't depend on eachother. If you need to alter one service, as long as its inputs and outputs remain the same, do not affect the other services. 

Microsoft as a great write-up: https://learn.microsoft.com/en-us/azure/architecture/microservices/

Amazon is a great example: when you order something via the website, your order arrives at the Recieve Order microservice, that then dispatches an event to other services like fullfillment and shipping. DDD is a method to simplify this type of interaction. Great for systems that can span years, and interact with many different departments. Each department might have a different understanding of the same concept: An "order" in the web department might include IP address, where "order" in the shipping department might include "tracking number". Amazon and Netflix use this type of approach. 

## What is Domain Driven Design (DDD)? 

DDD is a method for architecting and building microservice systems. Invented by Eric Evans. It walks you through finding service-boundaries. 



![alt text](https://docs.microsoft.com/en-us/azure/architecture/microservices/images/monolith/figure2.png)


