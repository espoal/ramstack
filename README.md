# RAMStack
## Introduction

Ramstack is a collection of guidelines to build a full stack for web and natives apps, with the following characteristics:

 - ***Reliability***: The app is predictable, in correctness and performance, even in the presence of errors. The stack is capable of self-healing hardware and software faults.
 - ***Availability***:  The app is capable of overcoming faults in the stack and keep functioning, eventually returning to a consistent state. 
 - ***Maintainability***: Fixing bugs and adding new features should be easy. Developers can use any tool they prefer and it's easy to adapt to changing business requirements.

The stack as a whole aims to be ***anti-fragile***: an increase in load will be met with an increase in reliability and availability, faults are used to adapt robustness thresholds, big data is at the center of future business decisions.

One of the main ideas behind this stack is to move the load balancer and part of the cache in the client, thus creating a ***smart client***, decoupled from the frontend, to provide an offline-first experience and optimal performance. This can be seen as an evolution and extension of Google's PWA guidelines.

## Why RAMStack?

### Performance is a feature

99% 100 ms, 99.9% availability = Disaster

### Availability means trust

Slow = unreachable = lost costumer

### Business speed is crucial

requirements changes, and the tech should follow not drive

### Machine learning to the rescue

Log monitoring, time series predictions, UX tracking.

## Where are the libraries?

### Stay close to the metal

JQuery was king, JS fatigue

### Backend: Node.JS and Rust

rapid prototyping vs performance and safety

### Frontend: Javascript and React

The frontend bread and butter

### Databases: MongoDB and Redis

Scalability and performance

## Frontend

![enter image description here](https://raw.githubusercontent.com/espoal/ramstack/master/assets/back_front.svg)

### Smart Client, Fetch patching and HTTP 304

The traditional way to scale web services is to use load-balancers and caches. Typically once a single server can't handle anymore the work, the domain will be rerouted to a service whose sole purpose is to spread the load, locally or over the network. Common examples are Nginx in a reverse proxy configuration, HAproxy, or dedicated hardware solutions.

My idea is to move the load-balancer inside the client, hence the  _smart client_  name, exploiting Service Worker capabilities to patch fetch requests and reroute them to cache, if possible, or to the best endpoint according to latency and load. Here's a flow diagram of how requests are handled:

![The Fetch Flow](https://raw.githubusercontent.com/espoal/ramstack/master/assets/fetch_flow.svg)



### Render Stack: a functional approach

Functional programming has become popular in the Javascript world thanks to React, but is well suited to front end programming in general. Pure functions are functions that will always have the same output given an input, i.e. they do not depend on and do not have an internal state, thus allowing us to build easily testable components.  

Another advantage of pure functions is that they pair very well with caches. Given a cached state, I can easily hydrate it by running a render function, compared to OOP where you have to patch the internal state of Objects, leading to many mistakes.  

The render loop could be something like:

```
Insert Render loop
```

Since render is a pure function that depends only on the state, we can bootstrap the DOM by using a default and then stream the result. We are using an async iterator so that we don't have to wait for the function to complete, instead we can serve the content as soon as it's ready, for example by loading the head tag as soon as possible we can start prefetching scripts, CSS and images.  

In case of an event (URL change, form submission, ....) a new state is generated using an event handler. Again we are using an async iterator because there might be multiple long requests, and we don't want to wait for all of them to complete before we can start rendering. The conciliate function is responsible for updating the state, maybe using a diffing algorithm, and then pass the result to the render function that can surgically update the changed components.  

The render is itself an async iterator, so it can yield to the main thread between updates, even if they are the result of a single event, allowing for a 60 fps experience even on resource constrained devices.

#### User Segmentation

It's important to segment our user base according to their browser capabilities, optimally by sniffing the request headers or by using conditional imports:

-   Shared Worker: Browsers that support sharing threads across tabs. Roughly 33% of the market.
-   Service Worker: Browsers that support patching fetch requests inside a service worker. Cross-tab communication resource sharing can be achieved using IndexedDB. Roughly 60% of the market.
-   No Javascript: In case a browser doesn't fall in the previous two categories, we can provide a JS-less experience, with pages rendered server-side. A lot of functionalities usually achieved through JS can be done in  [CSS instead](https://github.com/you-dont-need/You-Dont-Need-JavaScript), making the page much faster for every user. This work can also be used to bootstrap a Google AMP implementation.

Other features useful to segment the user base are:

-   ECMAScript support: Usually developers use Babel to compile the code to the minimum common denominator, thus creating huge and bloated Javascript files.
-   Compression support: Brotli is a new compression algorithm, which is much better.
-   Media support: Even though the web seems to be converging toward WebP, it's useful the differentiate media support and serve only the best format at the optimal resolution.

## Backend

![enter image description here](https://raw.githubusercontent.com/espoal/ramstack/master/assets/fetch_flow_backend.png)

## Hybrid Cloud

### Bare metal or PaaS?

One common question that often comes up when architecting the backend: Should we use bare metal servers or a PaaS provider?  

A PaaS provider like AWS can significantly reduce time to market, tie the cost to actual usage and allow to delegate a large portion of system maintenance. On the other hand this comes at a high price point, and a skilled linux engineer is still required to manage everything.  

A good compromise is to use a hybrid cloud approach, where we identify a baseline load to be served from bare metal servers, while PaaS is used to meet load spikes, which usually are predictable:

### Scaling up or out?

When I started working on scaling backends, around 7 years ago, the typical server specs were: 4 core / 8 threads, 250-500 mbit/s bandwidth, 32 GB of RAM, 2x SATA SSD. The x86 market has stagnated a bit in the meanwhile, with moderate IPC increases year over year and a stable core count. Thankfully AMD recently introduced a competitive architecture, and one now can find hexa-core and octa-core servers in the same price bracket. The average NIC today is 1 Gigabit/s, with higher capacity available for a premium. SSDs on the other hand made huge leaps, especially with the switch to PCIe interfaces.  

In general it's rarely worthwhile to scale up, as hardware prices grow much faster than capacity. If one has the choice he should always choose to scale out instead, leaving scaling up to yearly server updates that leverage the normal market evolution.

### Unit Layout



### C10M problem with 300 euros per month


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExOTM0ODcxMTUsMTcwNjI3NTgzNiwtMT
k5MzE2Mzc1MSw4NjY3ODE3NTYsNDI1ODQ3MDA4LC00OTgwNzc3
ODIsMjA3MzM4NzY5MSw1MTUyMjk2OTAsODg3MTU5NzQxLC05Nz
c0NTY0MjYsODE3MzEwMDM2LDMzNjQwNzc5NywtMjAwNDM0MDU5
LC0xODc3NTk1Mjc1XX0=
-->