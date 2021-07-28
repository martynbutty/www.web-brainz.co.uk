# Architecture Notes
Search for "ship called the Vasa"...

## Anti-Patterns
* Cover your assets - Avoiding making any decision for fear of making the wrong one
* Groundhog day - nobody understands why a decision was made so it keeps getting discussed over and over (hint - ADR's)
* Email driven architecture - People forget / lose / don't know / didn't read / weren't around when an email of architecture 
  decision sent, therefore don't implement it correctly

## Architecture Patterns
E.g. CQRS is a pattern, but not a style. The difference spans from questions like "is CQRS a pattern, and is microkernel 
different fromCQRS?" I.e. you can deploy a pattern like CQRS into systems using the architectural styles like microservices, 
space based, event driven and modular monolith etc.

## Architectural Characteristics
* A non-domain design consideration
* Influences some structural aspect of the design
* Critical or important to application success

## Architecture Styles

### Service Based Architecture
Is a hybrid to microservices. Well defined domains deployed as separate units. Shared data like modular monolith (unlike
microservices where each service owns its own data)

### Modular Monolith
Becoming more popular. Single deployment unit with functionality grouped by domain. Popular with DDD.

Can be a good start point to get something out the door to prove it, save money, evolve the architecture or if you're just 
not sure if a distributed architecture will work.

Next step might be to move to **service based architecture:**

* Take all the domain area's (e.g. by namespace in code like app.customer.*)
* Pull them individually out of the modular monolith so they's an independently deployable unit of software (but shared DB maybe)
* Look at each of these domains to see which could/should be deployed as single purpose functions (i.e. **microservices**)

### Monoliths
SOA and Layered are still viable in the right place. Especially if using integrated communications between heterogeneous 
enterprise systems (ESB). So a micro frontend using REST and JSON can invoke a request that goes all the way down to old 
legacy "stuff" eg a Cobol mainframe / AS400 / C++, then it comes all the way back up the layers.

### Event-Driven
Is the latest hype, even though it's a fairly old architecture style. **Reactive **architecture, more complex and 
non-deterministic. Workflows are pushing this trend. Lots of complexity like testing and event timing.

### Space Based
Comes from the computer science term "tuple space". Multiple parallel processors with shared memory. Therefore all 
transactional data is cached in memory and DB is not used in the interactions of transactional processing. Provides 
highest volumes of elasticity, scalability and performance out of any of the architectural styles, because it removes 
the DB limiting constraint (bottleneck).

### Microservices Challenge
How to manage the transactionality when data is split between different bounded contexts?

Encapsulate business behaviour behind a platform, e.g. a group of microservices behind an API layer. The API layer can 
have a slow rate of change, therefore introducing stability and reuse.

### Hybrid Architecture
Service based, microservices architecture. Where not all of a system have to be microservices. Do all the area's meet the 
characteristics of microservices?

Microservices-event driven (or Event driven microservices)

## Distributed Architecture Consdierations

## The Fallacies of Distributed Computing
Suggested by L. Peter Deutsch and colleagues from Sun Microsystems in 1994, these fallacies still hold worthy consideration
today. [Ref: https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing]

### The Network is Reliable
Do not assume that the network is reliable, even though they have become more reliable over time, they remain generally 
unreliable. Distributed architectures rely on the network for communication between services. Even though all the services 
may be up and healthy, if they cannot communicate with each other, the system as a whole may not be healthy. Make sure
to consider things like timeouts and circuit breakers, to prevent phenomena like cascade failures.

### Latency is Zero
When you call some method in another service using something like REST or RPC, the measurment of time is usually in milliseconds.
 Compare that to internal method calls where we're measuring in nano or microseconds.

## Service Granularity

### Granularity Disintegrators
Reasons to separate services

* **Service functionality** (cohesion)
* **Code volatility** - do some parts not change much (git could show?). Would one service mean some aspect is down for 
  an unrelated change (e.g. deploy of something else)
* **Scalability and Throughput** - mean time to start (MTTS). Does one thing take a long time to start but others are 
  really quick? E.g part of a system that searches for printers for a letter print and send aspect
* **Fault Tolerance** - If one aspect goes down a lot, it would take other aspects down that are grouped into the single 
  service - mean time to recovery (MTTR)
* **Data Security** - would one aspect benefit from more or greater security

### Granularity Integrators

Favours monoliths. Converse of above granularity disintegrators, i.e. here are reasons to combine services

* DB transactions - Do you need ACID more than something else?
* Workflow choreography - network, security and data latency. Big ball of "distributed" mud. E.g. few ms for security 
  processing, few more for network, more still for data, multiplied by "n" calls per second means a potential large 
  cumulative latency. This can become worse still if you need timeout-retries, data consistency considerations etc
* Data dependencies - If two services need the same data, might they be better as a single service to avoid calling each 
  other and the data consistency problem therin