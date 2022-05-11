# Econometrics

Econometrics is the application of statistical methods to economic data in order to give empirical content to economic relationships.

# TRADEOFFS: relational and non-relational databases

SQL is a query language, whereas MySQL is a relational database that uses SQL to query a database

a database, like a MySQL database, is just a bunch of tables aka a relational database

<img src="/content/SQLvsNOSQL.png"/>

__relational databases:__

- hold data tables:

    - a collection of columns (headers) and rows (data)

- you can have multiple tables joined together by a defined relationship

- relationships help force constraints using primary keys and foreign keys

- table constraints: all the data is structured into a uniform manner

- storage is concentrated: 1 node that contains an entire copy of the data, not partitioned by default

- relational db scale can be either:

    - vertical: build a better machine via more memory, faster hard disk, better cpu

    - horizontal: simply add more machines

- relational db access uses raw SQL

__non-relational databases:__

- non-relational databases work best when data is distributed over multiple servers to be built to scale with high performance & low latency

- the cost is that queries are less flexible

    - tables, documents, or graphs hold data together but CANNOT be joined together by a relationship

    - the data is handled by key-value stores where the user needs to know the key

    - best when the data model fits (graphs)

- storage relies on hashing function for the input and the result is used to identify the partition where the data is stored

- nonrelational db scale is easily improved by adding more partitions that function & improved independently

- access: many are no-sql databases that have their own CRUD (create, read, update, delete) functionality that rely on key-value stores

    - REST APIs are used to hit a specific endpoint that comes with certain functionality

# COMPETENCY: service-oriented architectures (SOA)

<img src="/content/soa.gif"/>

__SOA example: ticket payment system__

<img src="/content/soa_example.gif"/>

# COMPETENCY: MapReduce

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

# COMPETENCY: distributed cache

distributed cache is an optimization technique for faster responses with scalability  

![distributed cache problem to solve](/content/distributedCache_problemToSolve.gif)

cache should be added at a later stage in the system development cycle, but it should be considered in the system horizontally scaled architecture

__PROBLEM TO SOLVE__

with many servers comes larger latency, despite being able to provide for millions of users by handling millions of client-requests per second

![distributed cache solution](/content/distributedCache_cacheSolution.gif)

__any layer in the architecture can have cache__

CDN: Content Delivery Network

- cache where users do NOT have to download on every client-request for the same image or static asset

Local Cache:

- on service in-memory cache for faster responses to client-requests

__distributed cache architecture examples__

Layer Cache: Reddis or Memcached

- request cache layer validation before client-requests hit the database

![distributed cache architecture](/content/distributedCache_architectureCache.gif)

__cache invalidation issues__

designing cache, especially in a distributed architecture where multiple levels of cache in different layers, can be extremely hard to manage & may produce cache invalidation issues

1. update latency

![update latency](/content/distributedCache_updateLatency.gif)

2. cache misses

![cache misses](/content/distributedCache_cacheMisses.gif)

# COMPETENCY: cloud load balancing


# COMPETENCY: memory management

# COMPETENCY: processes

# COMPETENCY: threads

# COMPETENCY: synchronization

# COMPETENCY: paging

# COMPETENCY: multithreading

# COMPETENCY: internet fundamentals

> DNS lookup: get an ip address for a domain name/website URL

> computer/client makes a REQUEST to a server

> server processes that request

> server's response is compiling website

__DNS lookups__

The domain name system recursor gets the query and communicates with other domain name system servers in order go get the correct IP address. Once it’s located, the domain name system recursor will send the query to the three other domain name system servers. Next, the root server, designated as the Internet’s domain name system root zone, responds to requests sent in the root zone. A list of authoritative nameservers that correspond with TLDs gets sent back as a response.

The TLD nameserver will then store the second-level domain IP address and release the website’s IP address. The query gets sent to the domain’s nameserver, and finally, the authoritative nameserver can respond to the original domain name system query.

__TCP/IP__

TCP/IP is nonproprietary and, as a result, is not controlled by any single company. Therefore, the IP suite can be modified easily. It is compatible with all operating systems (OSes), so it can communicate with any other system. The IP suite is also compatible with all types of computer hardware and networks.

TCP/IP uses the client-server model of communication in which a user or machine (a client) is provided a service, like sending a webpage, by another computer (a server) in the network.

Collectively, the TCP/IP suite of protocols is classified as stateless, which means each client request is considered new because it is unrelated to previous requests. Being stateless frees up network paths so they can be used continuously.

The transport layer itself, however, is stateful. It transmits a single message, and its connection remains in place until all the packets in a message have been received and reassembled at the destination.

The TCP/IP model differs slightly from the seven-layer Open Systems Interconnection (OSI) networking model designed after it. The OSI reference model defines how applications can communicate over a network.

Network address translation (NAT) is the virtualization of IP addresses. NAT helps improve security and decrease the number of IP addresses an organization needs.

Common TCP/IP protocols include the following:

Hypertext Transfer Protocol (HTTP) handles the communication between a web server and a web browser.
HTTP Secure handles secure communication between a web server and a web browser.
File Transfer Protocol handles transmission of files between computers.

> The 4 layers of the TCP/IP model

TCP/IP functionality is divided into four layers, each of which includes specific protocols:

1. The application layer provides applications with standardized data exchange. Its protocols include HTTP, FTP, Post Office Protocol 3, Simple Mail Transfer Protocol and Simple Network Management Protocol. At the application layer, the payload is the actual application data.

2. The transport layer is responsible for maintaining end-to-end communications across the network. TCP handles communications between hosts and provides flow control, multiplexing and reliability. The transport protocols include TCP and User Datagram Protocol, which is sometimes used instead of TCP for special purposes.

3. The network layer, also called the internet layer, deals with packets and connects independent networks to transport the packets across network boundaries. The network layer protocols are IP and Internet Control Message Protocol, which is used for error reporting.

4. The physical layer, also known as the network interface layer or data link layer, consists of protocols that operate only on a link -- the network component that interconnects nodes or hosts in the network. The protocols in this lowest layer include Ethernet for local area networks and Address Resolution Protocol.

__to socket connections__

A socket is one endpoint of a two-way communication link between two programs running on the network. A socket is bound to a port number so that the TCP layer can identify the application that data is destined to be sent to.

__REQUEST/RESPONSE cycle__

> the requests & responses contain HTTP Headers, additional metadata for both request and responses

accept: acceptable content-types for response

cache-control: specify caching behavior

user-agent: information about the software used to make the request

__response status codes__

2xx - success
3xx - redirect
4xx - client error (user fault)
5xx - server error (not user fault)

__HTTP verbs: GET & POST__

> GET

useful for retrieving data
data passed in query string
should have no "side-effects"
can be cached
can be bookmarked

> POST

useful for writing data
data passed in request body
can have "side-effects"
not cached
cannot be bookmarked

__api (application programming interface)__

> a version of a website intended for computers to communicate with one another with code

apis allows users to get data from another application without needing to understand how that application functions

apis can often send data back in different formats: JSON or XML

# COMPETENCY: traversals

# COMPETENCY: divide and conquer

# COMPETENCY: breadth-first search vs. depth-first search