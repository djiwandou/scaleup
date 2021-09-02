# The Scaleup
A journey to build a scalable Saved Search system (and sub-systems)
contoh PR
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
    * [System Context Diagram](#system-context-diagram)
* [How the System Works](#how-the-system-works)
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
The design & arch. in this document are made on the basis of **C4 modelling** and **Arch. as a code approach** which then rendered using **PlantUML** engine.

[C4 modelling](https://c4model.com/#CoreDiagrams) is an abstraction-first approach to diagramming software arch. based on 4 system thinking levelling: Context, Containers, Components, Code.

[Arch. as a code](https://github.com/trilogy-group/arch-as-code) is an approach to manage system design and diagram into a .yaml like code thus make it transparent to versioning and many benefit of teamwork techniques, e.g. PR reviews, static code analysis, CI/CD, etc.

I used [PlantUML](https://github.com/djiwandou/C4-PlantUML) as the rendering engine for generating the diagram based on the [code](figures/). 
### Roadmap
| Version                | Description                                                                                    |
|------------------------|------------------------------------------------------------------------------------------------|
| Saved Search System v1 :mag: | Initial saved search system, letting other products save the search result. See [v1 Use Cases](#saved-search-system-v1-use-cases).  |
| Saved Search System v2 :mag::satellite: | Second version of the saved search system, not only accommodating connection to the internal but also to the external search framework. See [v2 Use Cases](#saved-search-system-v2-use-cases).                                                                                                 |
| Saved Search System v3 :satellite::gear:                        | Third version of the saved search system, the system grows itself as the universal plugin can be used either by internal or external (cross functional) products. See [v3 Use Cases](#saved-search-system-v3-use-cases).                                                                                              |

* Each of the version will relate to the iteration version / mutually agreed deliverables scope between squad -team and the respective Engineering Manager- with other stakeholders, e.g. Product Manager, Business Owners, etc.

* Each of the version will incorporate software development phases, including: Planning, Grooming, Development (Pre-Alpha), Alpha, Beta -if needed-, Live production. 

### Scope Assumptions and Constraints
> Gather requirements and scope the problem. Clarify use cases and constraints. Discuss assumptions.
#### Functional Requirements
* Saved search system allows users to save multiple filtering dimensions on a listing search
* Users will receive email alerts on regular intervals with regards to the listing search
* Alerts received by the users contain at most 10 entries across all saved search
* Each entry consists of: title, description, call to action link back to the website

#### Non-Functional Requirements
* Saved search system is reusable with future facing Products 
* The system should cater for multiple Products with each product has it's own data store and listing representation
* The system should scale to millions of requests daily

#### Constraints and assumptions

* Traffic is not evenly distributed
    * Popular saved search request should almost always be put in the cache
    * Need to determine how to expire/refresh
* Low latency between machines
* High throughput needs to be addressed
* Limited memory in cache
    * Need to determine what to keep/remove
    * Need to cache millions of saved search request
* 100 million requests per month ~ 40 requests per second, see [Scalability Page](scalability/README.md#rough-estimates) for more detail


#### Saved Search System v1 Use Cases
<p align="left">
<img width="392" alt="V1 system" src="https://user-images.githubusercontent.com/74530990/126574543-53e20b29-ce0a-48ef-b2cf-99082511e9b0.png">
<br/>
Saved search system V1 illustration
</p>

#### Saved Search System v2 Use Cases
<p align="left">
<img width="392" alt="V2 system" src="https://user-images.githubusercontent.com/74530990/126574545-2242c3b7-fa07-49a7-8b7d-45ac0a1e21d7.png">
<br/>
Saved search system V2 illustration
</p>

#### Saved Search System v3 Use Cases
Will be explained more detail on the next design section.

The focus on this version is making the Saved Search System to be **generally available (GA)** when the previous use cases are met, and an ecosystem of search-enabled plugins are available & stable.

## High Level Design
> Comprises of system context diagram and explanation on how the system work
### System Context Diagram
<p align="center">
    <img src="https://user-images.githubusercontent.com/74530990/126722232-ba9b754c-edfa-49a2-b425-7943260cabf3.png"/>
    <br/>
    Saved Search System Context Diagram V3 
</p>

See the diagram's code here [system context v3](figures/system-contextv3.puml)

### Product
Product here, depicted by **Product A, B, and C** is defined as the system where sometimes directly related to end users ("real" external users or another internal department). The Products can also be categorized as internal (development happened in-house or internally) or external (development externally either by third party or communities support).

Product sometimes consists of any of these modules (at least one component): 
* Frontend 
* Backend
* Mobile

### Saved Search System
This is the core of the system. **Saved Search System** comprises of several handlers and components in order to do its function properly, i.e. Product Listing Handler, Saved Search Handler, Search Framework Integrator, E-mail Handler, Alert Handler.

### External e-mail system
External e-mail system, is the system with sole purpose to deal with e-mail messages distribution to the users and its related properties: regularly set the email sending time, set email recipient, including more advanced features such as: get metrics on the email data, users segmentation, set campaign, etc. 
The example of external e-mail systems are: SaaS, Twilio, MailChimp, and GetResponse. 

### External search framework
This external search framework provides more advanced features of searching and its related properties, e.g. analytics, auto-completion, correcting typos, handling synoyms, advanced filtering, rating, etc.
The example of external search frameworks are: SaaS, Solr, Lunr, and possibly the most wellknown Elasticsearch. 

## How the System Works

### 1. Integration with Products
**Product Listing Handler** is the name of the component who will take care of the common integration with the Products. Each of the products will have their own respective listing -read: communication format, protocol, or even their own standardize "language"- as they are developed by another squads.

So, if the characteristics of each Products are unique, then we should do these processes inside the handler
1. Parsing: 
First, we need to define our own `Schema` or listing that describes which fields we are expecting from the incoming messages (listing data from the Products). 
Irrespective for each product's listing or schema, they need to follow the system's schema. In regards to this process, we could also register/re-define or set the main schema reference that is used in our system. 

Parsing is the process to get the required data from each product's listing and convert it into Saved Search System's own schema. 

2. Hydrating: 
Often, when we received incoming messages that has less than required data format. In this case, we will utilized `Hydrator` function that adds the required information in order to meet standardized `Schema`.
To sum up, hydrating is the process to "enrich" or "hydrate" the data to meet the minimum format.

3. Processing (Batching):
Then, after the data is ready, this handler will send the whole data, batch-processing and send it through the right channels to the Core **Saved Search Handler**.

### 2. Saved Search Handling & Dealing with External Search Frameworks
**Saved Search Handler** is the core of this system. 
These are the core's job:
> The main function for this handler is to save/store search listing as well as its included filtering dimensions, receiving the batch to-be-stored-data from [**Product Listing Handler**](#1-integration-with-products) 
> 
> As well as communicating with [**Search Framework Integrator**](#2-saved-search-handling-&-dealing-with-external-search-frameworks) to get better refined search and filtering results. 
> 
> And in the end of the day to send trigger (search-data & message properties) to [**E-mail Handler**](#3-communication-with-external-email-system) to deal with external communication to users.
> 
> In the internal communication side, this core needed to give updated status to [**Alert Handler**](#4-observation-and-monitoring) whether the whole Saved Search System status is OK or might be endangered. 


**Search Framework Integrator** is the sub-system with the aim to enable the capability to deploy Saved Search System using any search engine, by providing an integration and translation layer between the core :point_up_2: and search engine specific logic that can be extended for different search engines. 

#### Integration with Frontend or Mobile
This sub-system could be integrated using plugin-like approach for FE or Mobile. 
For example, we could declare the plugin via `gradleAPI()` as custom Gradle tasks or plugins for Mobile, e.g. Kotlin.
```
plugins {
    `saved-search-plugin-mobile`
}

repositories {
    mavenCentral()
}

dependencies {
    implementation("dubizzle.mod.savedsearch:3.1")
}
```
In the FE side, the plugin is JS-based could be added through npm installation
```console
$ npm i savedsearch-plugin-fe
```
or if this plugin will be installed globally, please add `-g` for the npm param
```console
$ npm i -g savedsearch-plugin-fe
```

As for the configurable parameters, I plan to put the param using separate `.yml` file as well as common environment variables:
```console
$ SAVEDSEARCH_ENABLED=true SAVEDSEARCH_ENGINE=savedsearch_config.yml
```


#### Integration with Backend
As the BE developer, the integration process more or less will be look similar to this example (in Golang):
```
package main

import (
	"context"
	"encoding/json"
	"fmt"

	saved-search "gopkg.in/dubizzle/savedsearch-plugin-be.v3"
)
func main() {
    /* get default search source defined by the plugin */
	searchSource := saved-search.GetSearchSource()
    /* init saved search list and add json-based query string -search keyword and filter- to list */
	searchSource.InitSavedList("name", "Doe")
    searchSource.AddSavedList(json.Marshal(queryStr))

    /* to get the search result from specific users and get it processed -email- based on Crontab script*/
    searchService := saved-search.Search().User("name", "Doe").SearchSource(searchSource)
    
	searchResult, err := searchService.GetSearchResult()
	if err != nil {
		fmt.Println("Error getting result: ", err)
		return
	}

    searchService.EmailProcessed(searchResult,"0 17 * * mon,wed")
}
```


### 3. Communication with External email System
In order to get better separation of concern and avoid Single Point of Failure (SPoF), more specialized handler is used to communicate to multiple external e-mail systems namely **E-mail Handler**.

For example, the system will have GetResponse, Twilio and MailChimp as the external e-mail systems. Thus, this handler will cover the direct interfacing layer to the system and translate the trigger (search-data and message properties ) received from the Core **Saved Search Handler** to each of the external system.

This Handler will also incorporate scalability pattern to get the most reliable external system in terms of Round-Robin application and Fail-over in case one of the external system fail to do the job then other will take-over. 

### 4. Observation and Monitoring
**Alert Handler** is the sub-system designated for communicating with **Main Alert System** for the purpose of observing and monitoring the Saved Search System overall lifecycle. 
The process inside this handler including, but not limited to: 
* set alert distribution
* customize alert message 
* set owner of the alert, e.g. security team, respective squad
* de-duplication
* automated follow up and metrics, e.g. give trigger to auto restart pod event when shutted down, auto scale, etc.

For the reference for **Main Alert System** I would like to give appreciation to [Spotify Comet alert framework](https://github.com/spotify/comet) as the main references. :clap: :clap:

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