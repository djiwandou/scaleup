# The Scaleup
A journey to build a scalable Saved Search system (and sub-systems)

## Motivation
About the author:
> Work with heart, we are human not cows 
> 
> Trying to balance between Quality & Pragmatism on software development.

## Index (Table of Content)
> This is the TOC ~ 
> Each sections contains my thinking journey and some references

* [Intro: My Initial Thoughts](#intro-my-initial-thoughts)
    * [Scope Assumptions and Constraints](#scope-assumptions-and-constraints)
* [General System Design](#general-system-design)
* [High Level Design](#high-level-design)
* [Detailed Components Design](#detailed-components-design)
    * [Saved Search Service](#saved-search-service)
    * [Alert Notif Service](#alert-notif-service)
* [API Design](#api-design)
* [Scale Up](#scale-up)
* [Future and Further Exploration](#future-and-further-exploration)

## Intro: My Initial Thoughts
<p align="center">
<img width="392" alt="early_problem" src="https://user-images.githubusercontent.com/74530990/126313113-120293ec-9ea2-4c54-ad97-e29123c6b2b2.png">
<br/>
Saved search early illustration
</p>
First thing on my mind when I was asked to build/architect a Saved Search System are these personal so-called "principles"

1. Architecting is a journey/process and it should be beyond original specs & requirements, I personally support the **Continuous Architecture** concept
2. Sometimes its OK to make quick & bold changes, especially if ~~something occurs~~ traffic trends toward the upper limit of the design capacity
3. Rely on data & metrics to make correct tech. design decisions
4. Ensure metrics are easy to observe and to understand
5. Workarounds are also OK, but don't keep it for too long because they are part of **Tech. Debts**

### Scope Assumptions and Constraints

* Re-state the problem/question

* Mind-map

* Who

* How

* Use Cases

## General System Design

### C4 

### Diagram as a Code

### Roadmap

## High Level Design

## Detailed Components Design

### Saved Search Service

### Alert Notif Service

## API Design

## Scale Up
<p align="center">
    <img src="https://user-images.githubusercontent.com/74530990/126078027-4ff93bb7-ee28-418a-b2cc-f205e59f4e8e.png"/>
    <br/>
    Scalability map, a range of techniques and patterns to scale-up the system
</p>
->see the diagram's code here [scalability map](figures/scalability-map.puml)<-

Scalability is a wide topic to cover, so I will explain more in [Scalability Page](scalability/README.md).

## Future and Further Exploration