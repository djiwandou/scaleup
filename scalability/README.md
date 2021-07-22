# Welcome to scalability page
> Hyperscale system attributes
> 1. Exponential growth in CPU & Storage
> 2. Linear growth rate in cost (build, operate, support, evolve)

## Rough Estimates 
* I assume each saved search query will be stored in key:value type of data
    * Key: user-Id, saved-search-Id, Value: saved search listings consists of search query including filter attributes
    * `user-id` - 10 bytes
    * `saved-search-id` - 10 bytes
    * `search-query` -  80 bytes 
        * `filter-attr1` - 20 bytes
        * `filter-attr2` - 20 bytes
        * `filter-attr3` - 20 bytes
        * `filter-attr4` - 20 bytes
    * Total:100 bytes
* Storage: 
    * 100 bytes * 100 million requests monthly if all value are uniques
    * **10 GB of storage**
* Bandwidth: 
    * 100 million requests monthly ~ 40 requests per second
    * 3.5 million requests daily
    * Each request needs around 100 bytes 
    * 100 bytes * 3.5 million requests daily
    * **100 MB of bandwidth**

Handy conversion guide: 
* 2.5 million seconds per month
* 1 request per second = 2.5 million requests per month
* 40 requests per second 100 million requests per month
* 400 requests per second = 1 billion requests per month
      


## Load Balancing
* To distribute the load received

## Caching
* Distributed Caching

* Where? on what side

* Reverse Proxy 
Mainly used for for interacting with third party, e.g. Lunr, Solr, ElasticSearch (external search framework), GetResponse, Twilio (external email system)

## Database
* Database Scaling

* Database choice

## Web Server

* Framework

## Code

* Documentation

* Linting

* Style check

* Hook

## Observability & Monitoring

* Pattern references for observability & monitoring

## Additional Concerns