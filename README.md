# Big O Notation

    /*
        ! Big(O) Notation / O(n): independent of hardware, an algorithm's TIME COMPLEXITY relative to the number of processed items
            Always measures WORST-CASE scenario

        ! Big(O) TIME COMPLEXITY: the worst case scenario for the number of steps in an algorithm's execution

        ! Big(O) SCALE MEASUREMENT: the algorithm's TIME COMPLEXITY performance as the number of processed items grows

        * Big(O) TYPES
        best-to-worst performance

            * O(1) = O of 1
               constant time complexity

            * O(logn) = O of log n to the base 2
               logarithmic time complexity

            * O(n) = O of n
               linear time complexity

            * O(nlogn) = O of n log n
               loglinear time complexity

            * O(n^2) = O of n-squared
               quadratic time complexity
     */

# Recursion

    /*
        ! RECURSION: an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)
            an algorithm is a repeatable sequence of steps

        ? RECURSION base case/breaking condition: the algorithm either upward propagates recursive call return for stack resolution or experiences a stack overflow

        * factorial example:
            after the downward recursive calls, the app stops the recursive calls upon reaching the base case:

                recursiveFactorial(0)

            then, each stack call resolves in an upwards direction from the return values

                !3 = 1*2*3 = 6

                    recursiveFactorial(3)
                            returns 3 * (2 * 1) = 6

                    recursiveFactorial(2)
                            returns 2 * 1

                    recursiveFactorial(1)
                            returns 1 * 1

                    recursiveFactorial(0)
                            returns 1

        * RECURSION factorial logic:

            !1 = !0 * 1 = 1

            !2 = 1*2 = !1 * 2

            !3 = 1*2*3 = !2 * 3

            !4 = 1*2*3*4 = !3 * 4

            !5 = 1*2*3*4*5 = !4 * 5

        * simplified factorial equation for RECURSION

            !n = !(n-1) * n

        ? DIVIDE & CONQUER

            recursively divide the original problem into 2 or more sub-problems & repeat until the sub-problems become small enough to solve a base case

            after solving the base case/breaking condition, combine the solutions to construct the overall solution to the original problem
     */

# Data Structures

## arrays

    /*
        ! ARRAYS: memory efficient because you don't have to store extra info with each element in the array

        ! TIME COMPLEXITY O(1) constant: when getting an element with index in an array
                step 1: multiply size of the element by its index
                step 2: get the start address of the array
                step 3: add the start address to the result of the multiplication
     */


## heaps

    /*
        ! HEAPS: a complete binary tree w/ array-backing, only interested in  min & max at ROOT of tree O(1) time complexity that functions left-to-right

            node at array[i]

                leftChild_index = 2i + 1

                rightChild_index = 2i + 2

                parent_index = floor((i-1) / 2)

            * ex: 15 at index_3 in [22, 19, 18, 15, 3, 14, 4, 12]

                leftChild_index = 2(3) + 1 = index_7 = 12

                rightChild_index = 2(3) + 2 = index_8 = out-of-bounds, so no child

                parent_index = floor((3-1) / 2) = index_1 = 19

        ! PRIORITY QUEUES HEAPS: max HEAP implementation w/ array backing always want the highest priority item first at O(1) constant time complexity
            insert() = add()
            poll() = remove()
            peak() = getRoot

        ! Java class PRIORITY QUEUE is a MIN HEAP = lower the number, the higher the priority
            FOR MAX HEAP: you'd need a comparator that will look at the two values and whenever you have one value greater than the other you in fact want to return that that value's less.

        ? HEAPIFY: the process of converting a binary tree into a heap after inserting or deleting a node

        ? HEAP peek(): O(1) constant time complexity to fix by swap replacement item up to root
            get root

        ? HEAP insert(): O(logn) logarithmic time complexity to fix by swap new item up to root

            step 1: always add to end

            step 2: heapify()

            step 3: compare new item against parent

            step 4: if greater than parent, then swap

            step 5: repeat

                * ex: add 20 as child to 15 parent

                                    22

                               19       18

                       15     3             14     4

                   12

                * since 20 is greater than 15 parent, swap

                                    22

                               19       18

                       20     3             14     4

                 12   15

                * since 20 is greater than 19 parent, swap, afterwards the complete tree has been HEAPIFIED()

                                    22

                               20       18

                       19     3             14     4

                 12   15

        ? HEAP delete(): O(logn) logarithmic time complexity to fix by swap replacement item up to root

            step 1: find replacementValue

            step 2: always take rightmost value to keep tree complete

            * only need to 3A or 3B, but not both
            step 3A heapify(): if replacementValue greater than parent, then fixHeapAbove, swap replacementValue w/ parent

            step 3B heapify(): if replacementValue lesser than parent, then fixHeapBelow, swap replacementValue w/ larger of two children

            step 5: repeat until replacementValue in correct index

                ! ex) delete 75; replacementValue 67

                                    80

                               75       60

                        68    55          40  52

                    67

                * deleted 75

                                    80

                               67       60

                        68    55          40  52

                * heapify() = fixHeapBelow

                                    80

                               68       60

                        67    55          40  52

                ! ex) delete 40; replacementValue 67

                                    80

                               75       60

                        68    55          40  52

                    67

                * deleted 40

                                    80

                               75       60

                        68    55          67  52

                * heapify() = fixHeapAbove

                                    80

                               75       67

                        68    55          60  52

        ? MAX HEAP: every parent has to have a value greater than or equal to its children in a complete binary tree

                Traversing down to every leaf, all the values along each path should be in descending order.

                                    22

                               19       18

                       15     3             14     4

                   12

        ? MAX HEAP SORT: sort nodes in a max heap

                step 1: root has the largest value

                step 2: swap root w/ last element in the array

                step 3: heapify(), excluding last node

                step 4: after heapify(), the second largest element is at the root

                step 5: repeat

                ! ex) max heap sort

                                    80

                               75       60

                        68    55          40  52

                    67
                                    67

                               75       60

                        68    55          40  52

                    80

                    * must heapify() index 0 - index 6

                                    75

                               68       60

                        67    55          40  52

                    80

                                     52

                               68       60

                        67    55          40  75

                    80

                    * repeat: must heapify() index 0 - index 5 until root index is left after heapify()

        ? MIN HEAP: every parent has to have a value that is less than or equal to its children in a complete binary tree

                Travelling from the root down to the leaves, all the paths would be in ascending order

                if you start at a leaf and travel up to the root, all the paths would be in descending order
     */

## LinkedLists

    /*
        ! ARRAYS: memory efficient because you don't have to store extra info with each element in the array

        ! TIME COMPLEXITY O(1) constant: when getting an element with index in an array
                step 1: multiply size of the element by its index
                step 2: get the start address of the array
                step 3: add the start address to the result of the multiplication
     */

## maps

     /*
        ? MAPS INTERFACE: collection of key-value pair HASHMAP implementations that use GENERIC CLASS dataStructures w/ 2 parameters: UNIQUE key & value
            GENERICS: improve OOP ENCAPSULATION by creating classes, interfaces, & methods that only take a specific dataType parameter;

        ? no-order HASHMAPS & LINKED HASHMAPS classes are the main implementations of the MAPS INTERFACE

            Map<dataType, dataType> instance = new HashMap<>()

        ? hashmapInstance.put(key, value) = add unique_key-value generics class pair into map collection

            ! if you add the key again, the oldValue will be overridden in the map since map keys are unique
                before overriding the value, .put() will return the previous value of the key-value pair
                a value being added for the 1st time will initially return null before adding to the map collection

        ? hashmapInstance.get(key) = retrieve record via key in map collection

        ? hashmapInstance.getOrDefault(key, defaultValue) = get the value mapped with specified key. If no value is mapped with the provided key then the default value is returned.

        ? hashmapInstance.containsKey(key) = validate key existence in map before adding/update key in map

        ? hashmapInstance.putIfAbsent(key, value) = for CONCURRENCY, if key is not already present in map, than add key-value pair

        ? Map.entrySet(): create a set out of the same elements contained in the hash map
        ? use hashmapInstance.keySet() + hashmapInstance.get(key) = loop through map & return all key-value pairs

        ? use hashmapInstance.remove(key) = remove key-value pair from map

        ? use hashmapInstance.remove(key, specificValue) = ONLY IF key has specific value, THAN remove key-value pair from map

        ? use hashmapInstance.replace(key, replaceValue) = IF key already exists, replace the key's value in the map

        ? use hashmapInstance.replace(key, validationValue, replacingValue) = ONLY IF key has specific value, THAN replace key's value in map

        ? HASHSET element/ HASHMAP key custom CLASSES: @Override .equals() & .hashcode() methods - if 2 objects compare equal, then they must have same collection bucket hashcode
     */

## queues

     /*
        ! QUEUE: (FIFO) first-in, first-out abstract class implemented by a LINKED LIST that uses enqueue(), dequeue(), peek()


            due to FIFO, no random access and can only access the top of a stack

            * add() or enqueue() = add value to end of the queue

                [10, 15, 4, 22]

                front = 10
                back = 22

                enqueue(20) = [10, 15, 4, 22, 20]

            * pop() or dequeue() = remove value from front of the queue

                [10, 15, 4, 22, 20]

                front = 10
                back = 20

               dequeue(20) = [10, 15, 4, 22, 20]

            * peek() = get item from front of queue


        ! STACK TIME COMPLEXITY:

            * O(1) CONSTANT TIME COMPLEXITY for push(), pop(), & peek() via LINKED LIST backing

            * O(n) LINEAR TIME COMPLEXITY for push(), pop(), & peek() via ARRAY backing

        ? CIRCULAR QUEUE: wrap back to front of the queue instead of resizing potentially front-empty queue

                ! The back field will always be pointing to the next available position in the queue.

                * adding to a full circular queue needs to be resized/doubled

                    1st iteration; back/nextAvailablePosition = index 5 for Bill

                        0 - jane - front
                        1 - john
                        2 - mary
                        3 - mike
                        4        - back

                    2nd iteration; back/nextAvailablePosition = index 7

                        0 - jane - front
                        1 - john
                        2 - mary
                        3 - mike
                        4 - bill
                        5
                        6
                        7         - back

                * wrap back to front & no need to resize array if removing & adding elements from a circular queue that's NOT full
                ! if circular queue is full, during 2x resize elements at the front of the queue assigned to back in order

                    1st iteration; back/nextAvailablePosition = index 2

                        0 - jane - front
                        1 - john
                        2        - back
                        3
                        4

                    2nd iteration; back/nextAvailablePosition = index 2 still after removing jane

                        0
                        1 - john - front
                        2        - back
                        3
                        4

                    3rd iteration; back/nextAvailablePosition = index 3 since adding

                        0
                        1 - john - front
                        2 - mary
                        3        - back
                        4

                    4th iteration; back/nextAvailablePosition = index 3 still after removing john

                        0
                        1
                        2 - mary - front
                        3        - back
                        4

                    5th iteration; back/nextAvailablePosition = index 4 still after adding mike

                        0
                        1
                        2 - mary - front
                        3 - mike
                        4        - back

                    6th iteration; back/nextAvailablePosition = index 4 still after removing mary

                        0
                        1
                        2
                        3 - mike - front
                        4        - back

                    7th iteration; back/nextAvailablePosition = index 4 still after adding bill

                        0        - back
                        1
                        2
                        3 - mike - front
                        4 - bill

                    nth iteration; back/nextAvailablePosition = index 2 but need unwrapping resize when adding gary

                        0 - jane
                        1 - john
                        2        - back
                        3 - mike - front
                        4 - bill

                    n+ iteration; back/nextAvailablePosition = index 5 but array has been doubled and elements in correct order

                        0 - mike - front
                        1 - bill
                        2 - jane
                        3 - john
                        4 - gary
                        5        - back
                        6
                        7

     */

## sets

    /*
       ? SETS INTERFACE: a computationally fast unordered collection without any duplicates implemented via HASHSET class

       ? SET UNION: a no-duplicate set that contains all the elements of 2 or more sets via hashSet.addAll()

       ? HASHSET equals() & .hashcode(): @Override both methods if using own object as map key or set element
    */

## stacks

    /*
        ! STACKS: (LIFO) last-in, first-out abstract class implemented by a LINKED LIST that uses push, pop, peek methods

            due to LIFO, no random access and can only access the top of a stack

        ! STACK O(1) CONSTANT TIME COMPLEXITY: for push(), pop(), & peek() via LINKED LIST backing

            O(n) LINEAR TIME COMPLEXITY for push(), pop(), & peek() via ARRAY backing
     */

## trees

    /*
        ! TREES: a collection of 1 parent nodes & their respective children connected by edges

            every item in a tree is a node

            * Red-Black Tree: self-balancing tree will validate balanced nodes after each traversal w/ insert(), delete(), & get() of O(n) linear time complexity

            ? singleton tree: a tree with only one child node
                ex: node 22 below

            ? edge: each of the single descending connections

            ? subtree: if you start at any given node & it's the node and all of its descendants.
                ex: node 4 below

            ? path: a no-cycle sequence of nodes required to go from one node to another, for example,
                ex: node 4 -> node 9 -> node 7 below

            ? node depth: number of edges to a node from the root node
                how many edges does it take me to get up to the root from the start node

                ex: node 14 has a depth of 3

                ex: node 18 has a depth of 2

            ? node height: the number of edges on the longest path from the node to a leaf.
                ex: node 4 has a depth of 2

                ex: leaf nodes has a height of 0

                ex: the rode/tree has a height of 3

            ? ancestor: child nodes in the given node's path
                ex: node 4 is an ancestor of 15

            * Tree example:
                            15 (root node) LEVEL ZERO

                22          4                17 LEVEL ONE

           19         9    18    3         11  0    LEVEL TWO

                  25   7          14           (leaf: a node that doesn't have any children) LEVEL THREE

        ! BINARY TREE TRAVERSAL: move between nodes in a tree data structure left-to-right

            ? LEVEL TRAVERSAL: visit nodes on each level left-to-right

            * level order: 25, 20, 27, 15, 22, 26, 30, 29, 32

                                    25

                               20       27

                          15    22        26  30

                                                29 32

            ? PRE-ORDER TRAVERSAL: visit the root of the subtree first left-to-right
                PRE = visit root first

            * pre-order traversal: 25, 20, 15, 22, 27, 26, 30, 29, 32

                                    25

                               20       27

                          15    22        26  30

                                                29 32

            ? POST-ORDER TRAVERSAL: visit the root of every subtree last left-to-right

            * post-order traversal: 15, 22, 20, 26, 29, 32, 30, 27, 25

                                    25

                               20       27

                          15    22        26  30

                                                29 32

            ? IN-ORDER TRAVERSAL: visit the left-child, then root, then right-child (repeat process for subtrees)

             * in-order traversal: 15, 20, 22, 25, 26, 27, 29, 30, 32

                                    25

                               20       27

                          15    22        26  30

                                                29 32

        ! TREE DELETE TRAVERSAL:

            * original:
                                     25

                               20       27

                          15    22        26  30

                          17                     29 32

            ? delete node is a leaf: null out parent node's left or right child

            * null out 17
                                     25

                               20       27

                          15    22        26  30

                                                29 32

            ? delete node has one child: save leaf value, delete leaf &  replace it's value at the respective parent node

            * deleted 17 and replaced parent node value 15 with 17

                                     25

                               20       27

                          17    22        26  30

                                              29 32

            ? delete node has two children: get the largest value in left-subtree or the smallest value in right-subtree

            step 1: look for replacement node for minimal disruption from EITHER (NOT both) left or right subtree

            step 2a: if left subtree selected, take the largest value from the left subtree

                    * deleteTargetNode: 20
                    * subTreeRoot: 15
                    * look for replacementNode starting at the root of the subtree of the deleteTargetNode (the max in leftSubtree)
                    * max: completely traverse left edges of a left subtree until discovering a node without a right child
                    * max: 17
                        if 17 had a left child, 17 replaces 20 & the left child replaces 17 node value

                    * null out node15 child

                                             25

                                       20       27

                                  15    22        26  30

                                  17                     29 32

                    * post-delete
                                             25

                                       17       27

                                  15    22        26  30

                                                         29 32

            step 2b: if right subtree selected, take the largest value from the right subtree

                    * deleteTargetNode: 27
                    * subTreeRoot: 30
                    * look for replacementNode starting at the root of the subtree of the deleteTargetNode (the min in leftSubtree)
                    * min: completely traverse right edges of a right subtree until discovering a node without a left child
                    * min: 29
                        if 29 had a right child, 29 replaces 27 & the right child replaces 29 node value

                    * null out node15 child

                                             25

                                       20       27

                                  15    22        26  30

                                  17                     29 32

                    * post-delete

                                             25

                                       17       29

                                  15    22        26  30

                                                          32
     */

## vectors 

    /*
        ! VECTORS are thread-safe ArrayList
            thread-safe = no conflict when using on different threads with manually having to synchronize the code (synchronization has overhead performance issue)

        ? use Vectors, if 1 or more threads are writing (CRUD) to an ArrayList there could be thread conflicts
     */

## Econometrics

Econometrics is the application of statistical methods to economic data in order to give empirical content to economic relationships.

## TRADEOFFS: relational and non-relational databases

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

# CONCURRENCY

the ability of software to execute processes simultaneously (one task doesn't have to complete before another one can start)

    Now that doesn't necessarily mean that the application is doing more than one thing at a time or at the same time, what it means is that progress can be made on more than one task.

BENEFITS

    BENEFIT 1:
        free up the main thread so that it can continue working and executing and you can report progress or accept user input and perform those other tasks on the screen or in other parts of the program,
        while another long-running task that we kicked off in another thread continues to execute in the background.

    BENEFIT 2: might want to use threads is because an API requires us to provide one.

        EXAMPLE:
            an application wants to download data and draw a shape on the screen.
            So if it's a concurrent application, what it can do is it can download a bit of data, then switch to drawing part of the shape and switch back to downloading some more data, then switch back to drawing more of the shape, and so on.

# PROCESS

an instance of a computer program with its own memory space that's sequentially executed by a computer system that has the ability to run several computer programs concurrently.

    java virtual machine instance ->
            the JVM runs as a process ->
                running a java console application ->
                    we're initiating said PROCESS

# THREAD

a unit of execution within a process, each process can have multiple threads, a method for a program to "split" itself into two or more simultaneously or pseudo-simultaneously running tasks.

    creating a thread doesn't require as many resources as creating a process.
    generally, a thread is contained inside a process and different threads in the same process share the same resources while different processes in the same multitasking operating system do not.

    every Java process or application has at least one thread and that's the main thread

    almost every java process also has multiple system threads that handle everyday tasks like memory management and input/output.
        for UI applications, this is just called the JavaFx application thread.

# MULTITHREADING:

the JVM is multi-processed and multithreaded and has background processes running while a single-thread (main) process/application is executing.

    So every process has a heap and every thread has a thread stack.

# SYNCHRONIZATION: 

the process of controlling when threads execute code and therefore when they can access the heap is called synchronization.

    When working with threads, we have to synchronize all areas where we think or where interference can happen.

! METHOD SYNCHRONIZATION: when a thread is executing the method, all other threads that want to call the method or any other synchronized method in that class will suspend until the thread running the method exits it. Then another thread can run a synchronized method then another, etc.

    if a class has three synchronized methods, then only one of these methods can ever run at a time and only on one thread.

    since only one thread can execute a synchronized method at a time, threads can't interleave when running a synchronized method.

    that prevents thread interference within synchronized methods, but not outside of those methods.

        if the same instance variables referenced within a synchronized method are also referenced outside it in code that multiple threads can run and that particular code isn't synchronized, then we may still see thread interference.

    In Java to synchronize a method, all we really have to do is add the synchronized keyword to a method declaration.

! STATIC OBJECT SYNCHRONIZATION: the intrinsic lock that's used is owned by the class object

    synchronize a block of statements that work with an object by forcing threads to acquire the object's lock before they execute the statement block.

    only one thread can hold the lock at a time, so other threads that want the lock will be suspended until the running thread releases it.

    Then one and only one of the waiting threads can get the lock and continue executing.
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

## COMPETENCY: traversals

BINARY TREE TRAVERSAL: move between nodes in a tree data structure left-to-right

> LEVEL TRAVERSAL: visit nodes on each level left-to-right

     * level order: 25, 20, 27, 15, 22, 26, 30, 29, 32

                             25

                        20       27

                   15    22        26  30

                                         29 32

> PRE-ORDER TRAVERSAL: visit the root of the subtree first then children left-to-right
         PRE = visit root first

     * pre-order traversal: 25, 20, 15, 22, 27, 26, 30, 29, 32

                             25

                        20       27

                   15    22        26  30

                                         29 32

> POST-ORDER TRAVERSAL: visit the root of every subtree last and children left-to-right first

     * post-order traversal: 15, 22, 20, 26, 29, 32, 30, 27, 25

                             25

                        20       27

                   15    22        26  30

                                         29 32

> IN-ORDER TRAVERSAL: visit the left-child, then root, then right-child (repeat process for subtrees)

      * in-order traversal: 15, 20, 22, 25, 26, 27, 29, 30, 32

                             25

                        20       27

                   15    22        26  30

                                         29 32

## COMPETENCY: divide and conquer

DIVIDE & CONQUER

- recursively divide the original problem into 2 or more sub-problems & repeat until the sub-problems become small enough to solve a base case

- after solving the base case/breaking condition, combine the solutions to construct the overall solution to the original problem

RECURSION

- an algorithm calls itself & each call is placed on the call stack waiting for a return value until the algorithm can no longer call itself (the base case/breaking condition)

  - an algorithm is a repeatable sequence of steps

- RECURSION base case/breaking condition

  - the algorithm either upward propagates recursive call return for stack resolution or experiences a stack overflow

divide & conquer algorithms are great for parallel processing because each sub-problem can be run on a different processor simultaneously (extremely performant on modern systems with large core counts)

POTENTIAL PROBLEMS
- make sure to avoid redundant recursive calls (solved via MEMOIZATION)

- MEMOIZATION: is a technique that can be used to improve the efficiency of divide & conquer algorithms by storing the solutions to earlier problems & eliminating redundant calls

DIVIDE & CONQUER EXAMPLES

1. Merge Sort

         ! Big(O) TIME COMPLEXITY: the worst case scenario for the number of steps in an algorithm's execution

             * LOGARITHMIC TIME COMPLEXITY = O(logn) = O of log to the base 2 n
                     repeatedly dividing array in half during splitting

         ! SPACE COMPLEXITY:

             * overall: NOT in-place

             splitting phase = in-place algorithm that doesn't use extra memory
                 track splitting via indices

             merge phase = NOT in-place algorithm
                 creates temporary arrays for sorting siblings for merge

         ! STABLE ALGORITHM:

             if there are duplicate elements, the original order of these elements will be preserved

                 because only swap if element at index_i > (index_i + 1)

         ! MERGE SORT LOGIC:

             * divide & conquer algorithm:

                 splitting base problem into several mini-problems, solving mini-problems, and then merging mini-solutions to solve base problem

             * recursive algorithm:

                 calls itself until reaching a base case and then feeds return values to itself to solve backwards

             ? PHASE 1: splitting

                 logical splitting (in-place = no new arrays)

                 1. divide the array into two sub-arrays (left & right partition)
                 2. then recursively divide each subsequent array into two arrays
                 3. UNTIL you have multiple sorted arrays of 1 length

                     split left side first, then right side last
                         each split results in 'sibling arrays'

                     EXAMPLE:

                                  [20, 35, -15, 7, 55, 1, -22]

                         [20, 35, -15]       &&            [7, 55, 1, -22]

                     [20]    &&  [35, -15]            [7, 55]    &&      [1, -22]

                                [35] && [-15]       [7] && [55]        [1] && [-22]

             ? PHASE 2: merging (not in-place)

                 MERGING = sorting elements starting from bottom-to-up with temporary array

                     not in-place: uses new temporary arrays

                 handle left side first, then right side

                     merge all sibling arrays on left & right side before proceeding to higher level to recursively merge resulting sibling arrays

                 STEPS:

                 1. create temp array that can hold all elements in the arrays we're merging

                 2. set i to 1st index of left sibling array

                 3. set j to 1st index of right sibling array

                 4. step through left & right array & get the smallest value for temp: compare left[i] to right[j] sibling arrays

                     if left[i] is smaller, copy to temp array and increment i by 1
                     if right[j] is smaller, copy to temp array and increment j by 1

                     repeat until temp array has merged all elements into temp array in sorted order

                 5. copy temp array back into original input array at the correct position (making it a STABLE algorithm)

                 6. repeat steps 4 & 5 until you have sorted original input array

2. Quick Sort

         ! Big(O) TIME COMPLEXITY: the worst case scenario for the number of steps in an algorithm's execution

             * LOGARITHMIC TIME COMPLEXITY = O(logn) = O of log to the base 2 n
                     repeatedly dividing array in half during splitting

         ! SPACE COMPLEXITY:

             in-place algorithm that doesn't use extra memory

         ! UNSTABLE ALGORITHM:

             if there are duplicate elements, no guarantee that their original order will be preserved,
                 since quick sort is predicated on moving elements around a pivotIndex for recursive partitions

         ! QUICK SORT LOGIC:

             * divide & conquer algorithm:
                 splitting base problem into several mini-problems, solving mini-problems, and then merging mini-solutions to solve base problem

             * recursive algorithm:
                 calls itself until reaching a base case and then feeds return values to itself to solve backwards

             ? PHASE 1: partitioning step/pivotIndex splitting

                 identify pivotIndex for logical splitting (in-place = no new arrays)

                     each element and it's respective index eventually serves as the pivotIndex

                     CHECK: pivotIndex serves as boundary for 2 sibling sub-arrays that prevent crossover

                 1. divide the array into two sub-arrays (left & right partitions)
                 2. then recursively divide each subsequent array into two arrays
                 3. UNTIL you have multiple sorted arrays of 1 length (each containing the pivotIndex element at it's correct position)

                     in left sub-array, elements less than pivotIndex element are moved to the left during traversal
                     in right sub-array, elements greater than pivotIndex element are moved to the right during traversal

                     AS A RESULT, element at pivotIndex will be in the middle AND in its correct position

                     EXAMPLE:

                                                      [20, 35, -15, 7, 55, 1, -22]

                                     [-15, 7, 20, 35]       pivotIndex = 7            [-22, 1, 7, 55]

                     [-15, 7]    pivotIndex = 7  [7, 20, 35]            [-22, 1]    pivotIndex = 1      [1, 7, 55]

             [-15] && [7]     [7, 20] pivotIndex = 20 [20, 35]       [-22] && [1]        [1, 7] pivotIndex = 7 [7, 55]

                             [7] && [20] && [35]                                     [1] && [7] && [55]

                 STEPS:

                     STEP 1: identify pivotIndex for 2-or-more element arrays
                         pivotIndex is the correct position in the sorted array

                     STEP 2: use recursion to subsequently partition the left & right partitioned arrays into more sub-arrays using the pivotIndex
                         BREAK CASE for recursive calls: handle 1 element arrays

                         using the first element respective index in the array as the pivotIndex

                         for left partition, search/traverse from left to right
                         for right partition, search/traverse from right to left
                         stop traversal when i and j cross each other to maintain partitions

                         FOUND 1st element less than pivot during traversal of LEFT partition: so move elements at index j to index i (move to LEFT of pivotIndex)
                         FOUND 1st element greater than pivot during traversal of RIGHT partition: so move elements at index i to index j (move to RIGHT of pivotIndex)

                         after correct index for pivotIndex element has been FOUND after each traversal, re-assign pivotIndex for subsequent sub-arrays/partitions

             ? PHASE 2: merging

                 MERGING = sorting elements/pivotIndex in respective 1-element array that are starting from bottom-to-up in-place

                 handle left side first, then right side

                     merge all sibling arrays on left & right side before proceeding to higher level to recursively merge resulting sibling arrays

                     after correct index for pivotIndex element has been FOUND after each traversal, re-assign pivotIndex for subsequent sub-arrays/partitions

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