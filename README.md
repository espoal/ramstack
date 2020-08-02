# RAMStack
## Introduction

Ramstack is a collection of guidelines to build a full stack for web and natives apps, with the following characteristics:

 - ***Reliability***: The app is predictable, in correctness and performance, even in the presence of errors. The stack is capable of self-healing hardware and software faults.
 - ***Availability***:  The app is capable of overcoming faults in the stack and keep functioning, eventually returning to a consistent state. 
 - ***Maintainability***: Fixing bugs and adding new features should be easy. Developers can use any tool they prefer and it's easy to adapt to changing business requirements.

The stack as a whole aims to be ***anti-fragile***: an increase in load will be met with an increase in reliability and availability, faults are used to adapt robustness thresholds, big data is the center of future business decisions.

One of the main ideas behind this stack is to move the load balancer and part of the cache in the client, thus creating a ***smart client***, decoupled from the frontend, to provide an offline-first experience and optimal performance. This can be seen as an extension of Google's PWA guidelines.

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

### Node.JS and Rust

rapid prototyping vs performance and safety

### Javascript and React

The frontend bread and butter

### MongoDB and Redis

Scalability and performance

## Frontend

## Backend

## Hybrid Cloud

### Scaling up or out?

When I started working on scaling backends, around 7 years ago, the typical server specs were: 4 core / 8 threads, 250-500 mbit/s bandwidth, 32 GB of RAM, 2x SATA SSD. The x86 market has stagnated a bit in the meanwhile, with moderate IPC increases year over year and a stable core count. Thankfully AMD recently introduced a competitive architecture, and one now can find hexa-core and octa-core servers in the same price bracket. The average NIC today is 1 Gigabit/s, with higher capacity available for a premium. SSDs on the other hand made huge leaps, especially with the switch to PCIe interfaces.  

In general it's rarely worthwhile to scale up, as hardware prices grow much faster than capacity. If one has the choice he should always choose to scale out instead, leaving scaling up to yearly server updates that leverage the normal market evolution.

### C10M problem with 300 euros per month


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ5ODA3Nzc4MiwyMDczMzg3NjkxLDUxNT
IyOTY5MCw4ODcxNTk3NDEsLTk3NzQ1NjQyNiw4MTczMTAwMzYs
MzM2NDA3Nzk3LC0yMDA0MzQwNTksLTE4Nzc1OTUyNzVdfQ==
-->