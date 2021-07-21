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
* [General System Design](#general-system-design)
    * [C4 and Architecture as a Code](#c4-and-architecture-as-a-code)
    * [Roadmap](#roadmap) 
    * [Scope Assumptions and Constraints](#scope-assumptions-and-constraints)
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

## General System Design

### C4 and Architecture as a Code
The design & arch. in this document are made on the basis of **C4 modelling** and **Arch. as a code approach** which are rendered using **PlantUML** engine.

[C4 modelling](https://c4model.com/#CoreDiagrams) is an abstraction-first approach to diagramming software arch. based on 4 system thinking levelling: Context, Containers, Components, Code.

[Arch. as a code](https://github.com/trilogy-group/arch-as-code) is an approach to manage system design and diagram into a .yaml like code thus make it transparent to versioning and many benefit of teamwork techniques, e.g. PR reviews, static code analysis, CI/CD, etc.

I used [PlantUML](https://plantuml.com/) as the rendering engine for generating the diagram based on the [code](figures/). 
### Roadmap
| Version                | Description                                                                                    |
|------------------------|------------------------------------------------------------------------------------------------|
| Saved Search System v1 :mag: | Initial saved search system, letting other products save the search result. See [v1 Use Cases](#saved-search-system-v1-use-cases).  |
| Saved Search System v2 :mag::satellite: | Second version of the saved search system, not only accommodating connection to the internal but also to the external search framework. See [v2 Use Cases](#saved-search-system-v2-use-cases).                                                                                                 |
| Saved Search System v3 :satellite::gear:                        | Third version of the saved search system, the system grows itself as the universal plugin can be used either by internal or external (cross functional) products. See [v3 Use Cases](#saved-search-system-v3-use-cases).                                                                                              |

* Each of the version will relate to the iteration version / mutually agreed deliverables scope between squad -team and the respective Engineering Manager- with other stakeholders, e.g. Product Manager, Business Owners, etc.

* Each of the version will incorporate software development phases, including: Planning, Grooming, Development (Pre-Alpha), Alpha, Beta -if needed-, Live production. 

### Scope Assumptions and Constraints
#### Saved Search System v1 Use Cases

#### Saved Search System v2 Use Cases

#### Saved Search System v3 Use Cases
Will be explained more detail on the next design section.

The focus on this version is making the Saved Search System to be **generally available (GA)** when the previous use cases are met, and an ecosystem of search-enabled plugins are avilable & stable.

## High Level Design

## Detailed Components Design

### Saved Search Service

### Alert Notif Service

## API Design
<p align="center">
    <img src="https://user-images.githubusercontent.com/74530990/126529996-dbe21105-951b-4ae3-89bb-a97ab649c984.png"/>
    <br/>
    API Design Considerations, things to lookup when designing API
</p>

See the diagram's code here [api design](figures/api-design.puml)
## Scale Up
<p align="center">
    <img src="https://user-images.githubusercontent.com/74530990/126078027-4ff93bb7-ee28-418a-b2cc-f205e59f4e8e.png"/>
    <br/>
    Scalability map, a range of techniques and patterns to scale-up the system
</p>

See the diagram's code here [scalability map](figures/scalability-map.puml)

Scalability is a wide topic to cover, so I will explain more in [Scalability Page](scalability/README.md).

## Future and Further Exploration

Throws back to my personal principle :point_up_2: [#3 and #4](#intro-my-initial-thoughts) 
more to come... is always to make the next best tech. decision based on data and observability metrics.

And don't forget to keep exploring :punch: