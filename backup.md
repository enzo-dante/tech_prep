## COMPETENCY: service-oriented architectures (SOA)

![soa](/content/soa.gif)

__SOA example: ticket payment system__

![soa example](/content/soa_example.gif)

## COMPETENCY: MapReduce

MapReduce is a parallel processing technique for processing a big data set which is distributed on a commodity cluster, instead of using serial processing.

Hadoop and MapReduce are most popular packages

__2-PHASE STRATEGY: map & reduce__

![mapPhase](/content/mapReduce_mapPhase.gif)

CREATE MAPS:

- mappers map input key/value pairs to a set of intermediate key/value pairs

- the maps are the individual tasks that convert input records into intermediate output records

SHUFFLE MAPS TO REDUCERS:

- send the mapper's intermediate output records to the reducers

![reducerPhase](/content/mapReduce_reducePhase.gif)

ASSIGN REDUCER RESPONSIBILITY/TASK:

- all same-key intermediate output values from mapper are presented to a single reducer together

```json

key = city name
list = each element/record that has data & shared key
reducerTask = for each team per division, get total annual sales (12 months)

reducerPacificWest: {

    suns: [
            [9,5,2,3,6,4,1,5,9,7,1,3],
            suns
        ],

    warriors: [
            [1,5,5,3,6,4,1,4,1,4,2,9],
            warriors
        ],

    clippers: [
            [3,5,2,9,6,4,1,7,5,9,8,3],
            clippers
        ],

    kings: [
            [6,8,2,8,6,4,1,5,2,7,1,1],
            kings
        ]

}
```

SMALL VALUE SET REDUCTION:

- process the data by adding data as final output result

__EXAMPLE: amazon wants to calculate its total sales city wise for the year 2015 in India__

![mapReduceExample](/content/mapReduce_exampleAmazon.gif)

2-phase strategy: map & reduce

![mapPhaseAmazon](/content/mapReduce_mapPhaseAmazon.gif)

![reducePhaseAmazon](/content/mapReduce_reducePhaseAmazon.gif)

## COMPETENCY: distributed cache

distributed cache is an optimization technique for faster responses with scalability by reducing multi-server latency by adding multi-level cached data validation

![distributed cache problem to solve](/content/distributedCache_problemToSolve.gif)

cache should be added at a later stage in the system development cycle, but it should be considered in the system horizontally scaled architecture

__PROBLEM TO SOLVE__

with many servers comes larger latency, despite being able to provide for millions of users by handling millions of client-requests per second

![distributed cache solution](/content/distributedCache_cacheSolution.gif)

__any architecture layer caching__

CDN: Content Delivery Network

- cache where users do NOT have to download on every client-request for the same image or static asset

Local Cache:

- on service in-memory cache for faster responses to client-requests

__distributed cache architecture__

Layer Cache: Reddis or Memcached

- request cache layer validation before client-requests hit the database

![distributed cache architecture](/content/distributedCache_architectureCache.gif)

__cache invalidation issues__

designing cache, especially in a distributed architecture where multiple levels of cache in different layers, can be extremely hard to manage & may produce cache invalidation issues

1. update latency

![update latency](/content/distributedCache_updateLatency.gif)

2. cache misses

![cache misses](/content/distributedCache_cacheMisses.gif)

## COMPETENCY: cloud load balancing

backend optimization technique to reduce cost & latency and improve performance & security

![cloud load balancing architecture](/content/cloudLoadBalancing_architecture.gif)

benefits:

- cross-regional failover

- fast autoscaling

- scales to millions of queries/requests per second

__PROBLEM TO SOLVE__

How do you scale, optimize, & secure a global app while maintaining low-latency for positive user experiences?

![local load balancing](/content/cloudLoadBalancing_localLoadBalancing.gif)

__cloud load balancing architecture__

layer 7 external/global load balancing

![layer 7 global load balancing](/content/cloudLoadBalancing_globalLoadBalancing.gif)

layer 4 internal load balancing

![layer 4 internal load balancing](/content/cloudLoadBalancing_internalLayer4.gif)

__data modeling__ 

layer 7 external/global load balancing

![data model layer 7](/content/cloudLoadBalancing_dataModelLayer7.gif)

layer 4 internal load balancing

![data model layer 4](/content/cloudLoadBalancing_dataModelLayer4.gif)

__security__

SSL Certificates

![certs](/content/cloudLoadBalancing_certificatesSecurity.gif)

prevent any layer attacks

![attack prevention](/content/cloudLoadBalancing_attackSecurity.gif)

## COMPETENCY: memory management

![cpu memory](/content/cpu_memory.gif)

__cpu (central processing unit)__

circutry in a computer that controls the manipulation of data that powers a computer via a small flat square called the motherboard

__cpu component: ALU (arithmetic logic unit)__

circutry that performs operations like addition & subtration on data 

__cpu component: control unit__

controls the ciruitry for coordinating all of the computer's activities

__cpu component: register unit__

which contains temporary memory for data

__volatile main memory/RAM (random access memory)__

temporary holding of software programs and apps and their associated data until the power is turned off

__non-volatile storage memory__

long-term holding of software programs and apps and their associated data even if the power is turned off

ex) memory sticks, hard disk drive, solid state drives(SSD)

## COMPETENCY: Page Memory & Paging

memory is split up into small, equal sized sections called pages (or page frames)

a single application may occupy multiple pages, which are not necessarily contiguous

each applications has its own view of the memory (logical memory)

a page table records where the different pages of a program are located in physical memory

unused pages may be paged out to a swap file on disc to make room for other

pages are paged in when needed again

supplementing physical memory with secondary storage is known as virtual memory

when memory is low, excessive swapping can lead to disc threshing & degrade performance

Part 1:

![paging part 1](/content/pageMemory_1.gif)

Part 2:

![paging part 2](/content/pageMemory_2.gif)

__page memory vs segmentated memory__

segmented memory makes an entire block of code available to processor which allows fast access

segmentation can lead to fragmentation of free space

with segmented memory, large processes may not get access to the memory very often

paged memroy can lead to fragmented processes which run more slowly

paged memory makes better use of free space

windows uses paged memory, segmented memory is not as common

## COMPETENCY: internet fundamentals

## COMPETENCY: breadth-first search vs. depth-first search

Use either search algorithm to recursively traverse a graph which is a collection of nodes where each node might point to other nodes that are connected via edges (one-way or two-way)

![graph](/content/graphs.png)

DEPTH-FIRST SEARCH

![depthFirstSearch1](/content/depthFirstSearch_part1.gif)

![depthFirstSearch2](/content/depthFirstSearch_part2.gif)

PROBLEM w/ DEPTH-FIRST SEARCH

![depthFirstSearchProblem](/content/depthFirstSearch_problem.gif)

IMPLEMENTATION: DEPTH-FIRST SEARCH

![depthFirstSearchImplementation](/content/depthFirstSearch_implementation.gif)

BREADTH-FIRST SEARCH

![breadthFirstSearch1](/content/breadthFirstSearch_part1.gif)

IMPLEMENTATION: BREADTH-FIRST SEARCH

![breadthFirstSearchImplementation](/content/breadthFirstSearch_implementation.gif)