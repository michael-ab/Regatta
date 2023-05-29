Carnegie Mellon University database systems course

Fall 2019:
https://www.youtube.com/playlist?list=PLSE8ODhjZXjbohkNBWQs_otTrBTrjyohi

Fall 2018 for 17-19 lectures:
https://www.youtube.com/playlist?list=PLSE8ODhjZXja3hgmuwhf89qboV1kOxMx7

## 01 - Relational model

## 02 - Advanced SQL

 GROUP BY:
![[Pasted image 20230515235041.png]]

HAVING:
![[Pasted image 20230515235745.png]]

## 03 - Database Storage I

### Page Layout
1. Tuple-oriented
![[Pasted image 20230519141253.png]]
2. Log-structured

## 04 - Database Storage II
 
![[Pasted image 20230519141412.png]]
![[Pasted image 20230519141726.png]]

### OLTP
![[Pasted image 20230519150507.png]]

### OLAP
![[Pasted image 20230519150530.png]]

### N-ARY Storage Model (NSM)

![[Pasted image 20230519151806.png]]

Pro/cons NSM
![[Pasted image 20230519152142.png]]

### Decomposition Storage Model (DSM)
![[Pasted image 20230519152227.png]]

![[Pasted image 20230519152340.png]]

Tuple identification for the DSM method. 
1. Use offsets no identify the tuple
2. Each attribute is embedded with the tuple I
![[Pasted image 20230519152725.png]]

Pro/cons DSM
![[Pasted image 20230519152935.png]]

## 05 - Buffer Pool - Memory Management

> [!NOTE] Title
> Memory part (not disk!)

![[Pasted image 20230519165553.png]]
Dirty flag: a bit to know if the page was modified 
Pin/Reference Counter: number of threads/queries currectly running that want this page in memory

Locks vs Latches
![[Pasted image 20230519170316.png]]

Page directory: (in disk) map page ID to page location in the database files
Page table: (in memory) map page ID to copy of the page in buffer pool frames
![[Pasted image 20230519170516.png]]

Allocation Policies
![[Pasted image 20230519182117.png]]

Multiple buffer pool
![[Pasted image 20230519182449.png]]

Multiple buffer pool
Approach: Object ID vs Hasing 
![[Pasted image 20230519182810.png]]

Scan sharing:
1. Queries can reuse data retrieved  from storage or operator computations.
2. Allow multiple queries to attach to a single cursor that scan a table.
![[Pasted image 20230519185946.png]]

Buffer pool bypass
![[Pasted image 20230519190359.png]]

### Buffer Replacement Policies 
1. Clock - Approximation of LRU without needing a separate timestamp per page
![[Pasted image 20230521163812.png]]

Problem with LRU and CLOCK (See example after)
![[Pasted image 20230521164005.png]]

2. Better policies: LRU-K
![[Pasted image 20230521164145.png]]

3. Better policies: localization
![[Pasted image 20230521164339.png]]

4. Better policies: priority hints
![[Pasted image 20230521164503.png]]

Dirty Pages
![[Pasted image 20230521164656.png]]

## 06 - Hash Tables

### Static Hashing schemes
1. Linear Probe Hashing
![[Pasted image 20230521172113.png]]

2. Robin Hood Hashing
![[Pasted image 20230521172955.png]]

3. Cuckoo Hashing
![[Pasted image 20230521173559.png]]

Chained Hashing
![[Pasted image 20230521180641.png]]

Extendible Hashing
![[Pasted image 20230521180710.png]]

Linear Hashing 
![[Pasted image 20230521180813.png]]

## 07 - Tree Indexes I

B+Tree properties
![[Pasted image 20230523115843.png]]

B+Tree example
![[Pasted image 20230523115943.png]]

B-Tree vs B+Tree
![[Pasted image 20230523120503.png]]

## 08 - Tree Indexes II

Inverted index stores a mapping of words to records that contain those words in the target attribute
![[Pasted image 20230526232210.png]]

## 09 - Multi-Threaded Index Concurrency Control

Locks vs Latches
![[Pasted image 20230528152646.png]]

Hash table latching
![[Pasted image 20230528153711.png]]

![[Pasted image 20230528153738.png]]

Latch crabbing/coupling
![[Pasted image 20230528154626.png]]

## 10 - Sorting & Aggregations

Query Plan
![[Pasted image 20230528161614.png]]

### Sorting algo

Issue for disk: we need to find a good sorting algo that don't do write too much data out the disk
![[Pasted image 20230529213842.png]]

External Merge Sort
![[Pasted image 20230529213856.png]]

2-way External Merge Sort
![[Pasted image 20230529214511.png]]

![[Pasted image 20230529214547.png]]

![[Pasted image 20230529214729.png]]

![[Pasted image 20230529214858.png]]

![[Pasted image 20230529215348.png]]

Using B+Tree for sorting
![[Pasted image 20230529215810.png]]

![[Pasted image 20230529215926.png]]

![[Pasted image 20230529220111.png]]

![[Pasted image 20230529220738.png]]

Hashing Aggregate
![[Pasted image 20230529221222.png]]

External Hashing Aggregate
![[Pasted image 20230529221258.png]]

![[Pasted image 20230529221421.png]]

![[Pasted image 20230529221655.png]]

![[Pasted image 20230529222004.png]]

![[Pasted image 20230529222207.png]]

![[Pasted image 20230529222342.png]]

## 11 - Join Algorithms


