## COMPETENCY: service-oriented architectures (SOA)

![soa](/content/soa.gif)

__SOA example: ticket payment system__

![soa example](/content/soa_example.gif)

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

paged memory can lead to fragmented processes which run more slowly

paged memory makes better use of free space

windows uses paged memory, segmented memory is not as common


