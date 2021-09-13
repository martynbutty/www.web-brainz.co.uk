---
title: Caching Strategies (with a focus on microservices)
description: caching strategies, topologies, eviction strategies etc from a microservice perspective
---
> Please Note - this page is a work in progress, so please check back here soon for further updates...
> 

## Topologies
### Distributed
A distributed cache is a client-server style cache. It's the cached data that is distributed, i.e. it's distributed between
all the services that use it, but there's only a single cache server/service.
* Uses a separate server (e.g. redis or ignite etc)
* All services using it use a client library to use the cache.
* Each service does not have cached data; It has to access it from the server
* Not fault tolerant, unless using a cluster

Can use:
IMDG
: In Memory Data Grid - Simple
IMDB
: In Memory DataBase - Can have a schema and thus be more complex, allows use of SQL like queries against the cached data

### Replicated
This type of caching topology requires no external server. The cached data resides in each service, in memory. The cache
 engine takes care of replicating the cached data amongst all instances, so it has "eventual consistency". Less products 
offer this type of caching compared to [Distributed](#Distributed), including [Ignite](https://ignite.apache.org/), 
[Hazelcast](https://hazelcast.com/use-cases/caching/), [GemFire](https://tanzu.vmware.com/gemfire), 
[Coherence](https://www.oracle.com/middleware/technologies/coherence.html) and 
others.

Eventual consistency is a by-product of how the cache operates. E.g after a "put" onto the cache, the cache engine updates
the other instances in the background. Some systems allow concepts like `syncout()` to force consistency, but this shouldn't
usually be necessary. The data replication engine (e.g. ignite) maintains a socket level connection to the other instances.

Beware of your cache size! For example on a shared host like when running kubernetes cluster, if you have 30 instances 
each with a 200MB cache, that's 6GB of data!.

Similar to above, this topology is not viable if you have large and/or lots of storage and/or instances.

### Near Cache
The near cache hybrid is a combination of a distributed and replicated cache. Each service has its own in memory cache, 
known as the front cache (or MRU, or MFU cache depending on the eviction strategy used - see later). There is also a 
distributed cache holding the full data set (or at least a larger dataset), known as the full or backing cache. 

* There are no communications between services for cache management like in a replicated cache, instead this is managed by 
the backing cache.
* It allows a large amount of cached data in the full (backing) cache
* It also allows a smaller subset of data in each service, in the front cache which might use MRU or MFU.
* It can suffer from inconsistent response times in some environments, especially in a microservice environment. This is
 because the data might not exist in the local front cache, so we have to go to the backing cache, and maybe even all the
 way to the database.
  
## Comparing Topologies
| | Replicated | Distributed | Near Cache |
|---|---|---|---|
| optimisation|performance|consistency|balanced|
| cache Size|small (<100 MB)|large (500MB +)|large (500MB +)|
| type of data|relatively static|transactional|relatively static|
| update frequency|relatively low|high|relatively low|
| fault tolerance|high|low|low|
| responsiveness|high|medium|variable|