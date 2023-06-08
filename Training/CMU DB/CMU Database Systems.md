Carnegie Mellon University database systems course

Fall 2019:
https://www.youtube.com/playlist?list=PLSE8ODhjZXjbohkNBWQs_otTrBTrjyohi

Fall 2018 for 17-19 lectures:
https://www.youtube.com/playlist?list=PLSE8ODhjZXja3hgmuwhf89qboV1kOxMx7

[[#01 - Relational model]]
[[#02 - Advanced SQL]]
[[#03 - Database Storage I]]
[[#04 - Database Storage II]]
[[#05 - Buffer Pool - Memory Management]]
[[#06 - Hash Tables]]
[[#07 - Tree Indexes I]]
[[#08 - Tree Indexes II]]
[[#09 - Multi-Threaded Index Concurrency Control]]
[[#10 - Sorting & Aggregations]]
[[#11 - Join Algorithms]]
[[#12 - Query Execution I]]
[[#13 - Query Execution II]]
[[#14 - Query Planning & Optimization I]]
[[#15 - Query Planning & Optimization II]]
[[#16 - Concurrency Control Theory]]
[[#17 - Two-Phase Locking Concurrency Control]]
[[#18 - Timestamp Ordering Concurrency Control]]
[[#19 - Multi-Version Concurrency Control]]
[[#20 - Database Logging Schemes]]
[[#21 - ARIES Database Recovery]]
[[#22 - Introduction to Distributed Databases]]
[[#23 - Distributed OLTP Databases]]
[[#24 - Distributed OLAP Databases]]
[[#25 - Shasank Chavan (Oracle In-Memory Databases)]]
[[#26 - Systems Potpourri]]


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

Why do we need to join?
![[Pasted image 20230529222901.png]]

Join Algorithms
![[Pasted image 20230529223010.png]]

Join Operator Output: Data
![[Pasted image 20230529225248.png]]

Operator Output - Record IDs
Called late materialization
![[Pasted image 20230529225611.png]]

I/O Cost Analysis
![[Pasted image 20230529230026.png]]

Join vs Cross-product
![[Pasted image 20230529230142.png]]

Join Algorithms
![[Pasted image 20230529230227.png]]

Nested loop join (for {for {}})
For every tuple in R, it scans S once
`cost: M + (m*N)`
![[Pasted image 20230529230451.png]]

Block Nested Loop Join
This algorithm performs fewer disk accesses
For every block in R, it scans S once
`cost: M + (M*N)`
![[Pasted image 20230529230838.png]]

Index Nested Loop Join
Assume the cost of each index probe is some constant C per tuple
`cost: M + (m*C)`
![[Pasted image 20230529231442.png]]

Sort-Merge Join
![[Pasted image 20230529231655.png]]

Sort-Merge Join Algorithm
![[Pasted image 20230529231812.png]]

Cost of Sort-Merge Join
![[Pasted image 20230529232132.png]]

Hash Join
![[Pasted image 20230529232509.png]]

Basic Hash Join Algorithm
![[Pasted image 20230529232649.png]]

![[Pasted image 20230529232748.png]]

Hash Table Contents
![[Pasted image 20230529232814.png]]

Hash Table Values
![[Pasted image 20230529232851.png]]

Bloom filter
![[Pasted image 20230529233058.png]]

Bloom filters
![[Pasted image 20230529233158.png]]

Grace Hash Join
![[Pasted image 20230529233745.png]]

Grace Hash Join
![[Pasted image 20230529234048.png]]

Recursive Partitioning
![[Pasted image 20230529234202.png]]

![[Pasted image 20230529234326.png]]

`Cost = 3(M+N)`
![[Pasted image 20230529234353.png]]

Join Algorithms: Summary
![[Pasted image 20230529234614.png]]


## 12  - Query Execution I

Processing model
![[Pasted image 20230530120316.png]]

1. Iterator Model (Also called **Volcano** or **Pipeline** Model)
![[Pasted image 20230530120416.png]]

![[Pasted image 20230530121516.png]]

Each time compute a single tuple
![[Pasted image 20230530122703.png]]

2. Materialization Model
![[Pasted image 20230530122313.png]]

Compute all tuples together
![[Pasted image 20230530122509.png]]

Better for OLTP
Not Good for OLAP
![[Pasted image 20230530122844.png]]

3. Vectorization Model
![[Pasted image 20230530123023.png]]

Each time compute a batch of tuples
![[Pasted image 20230530123149.png]]

Good for OLAP
![[Pasted image 20230530123252.png]]

Plan Processing Direction
![[Pasted image 20230530123419.png]]

Sequential Scan
![[Pasted image 20230530123721.png]]

Sequential Scan: Optimizations
![[Pasted image 20230530123843.png]]

Zone Maps
![[Pasted image 20230530124047.png]]

Late Materialization
![[Pasted image 20230530124436.png]]

Heap Clustering
![[Pasted image 20230530124539.png]]

Index Scan
![[Pasted image 20230530132238.png]]

![[Pasted image 20230530133331.png]]

Multi-index Scan (Bitmap Scan)
![[Pasted image 20230530133433.png]]

![[Pasted image 20230530133705.png]]

Multi-index scan example
![[Pasted image 20230530133804.png]]

Index Scan Page Sorting
![[Pasted image 20230530133917.png]]

Expression Evaluation (Expression tree)
![[Pasted image 20230530134236.png]]

## 13 - Query Execution II


Why Care About Parallel Execution?
![[Pasted image 20230530150704.png]]

Parallel vs Distributed
![[Pasted image 20230530150802.png]]

![[Pasted image 20230530150903.png]]

Process Model
![[Pasted image 20230530151209.png]]

![[Pasted image 20230530151405.png]]

1. Process Per Worker
![[Pasted image 20230530151433.png]]

2. Process Pool
![[Pasted image 20230530151630.png]]

3. Thread Per Worker
![[Pasted image 20230530151947.png]]

![[Pasted image 20230530152109.png]]

Inter- vs Intra-Query Parallelism
![[Pasted image 20230530152348.png]]

Inter-Query Parallelism
![[Pasted image 20230530152521.png]]

Intra-Query Parallelism
![[Pasted image 20230530152600.png]]

Intra-Query Parallelism
![[Pasted image 20230530152746.png]]


Intra-Operator Parallelism
1. Intra-Operator (Horizontal)
![[Pasted image 20230530171754.png]]

![[Pasted image 20230530172013.png]]

Exchange Operator
1. Gather
2. Repartition
3. Distribute
![[Pasted image 20230530172247.png]]

![[Pasted image 20230530172536.png]]

Inter-Operator Parallelism
2. Inter-Operator (Vertical)
Called pipelined parallelism
![[Pasted image 20230530172753.png]]

Example
![[Pasted image 20230530172833.png]]

3. Bushy Parallelism
![[Pasted image 20230530172935.png]]

I/O Parallelism
![[Pasted image 20230530173414.png]]

Multi-Disk Parallelism
![[Pasted image 20230530173611.png]]

Database Partitioning
![[Pasted image 20230530173704.png]]

Partitioning
![[Pasted image 20230530173938.png]]

Vertical Partitioning
![[Pasted image 20230530174113.png]]

Horizontal Partitioning
![[Pasted image 20230530174152.png]]

## 14 - Query Planning & Optimization I

Query Optimization
SQL is declarative 
![[Pasted image 20230601104932.png]]

Query Optimization:
1. Heuristics/Rules
2. Cost-based Search
![[Pasted image 20230601105149.png]]

Architecture Overview
![[Pasted image 20230601124001.png]]

Logical vs Physical Plans
![[Pasted image 20230601124059.png]]

Query Optimization is NP-HARD
![[Pasted image 20230601124328.png]]

Relational Algebra Equivalences
![[Pasted image 20230601124655.png]]

Predicate Pushdown
![[Pasted image 20230601124904.png]]

Relational Algebra Equivalences
![[Pasted image 20230601125126.png]]

![[Pasted image 20230601125453.png]]

## 15 - Query Planning & Optimization II

Cost-based Search
![[Pasted image 20230602153409.png]]

Cost Estimation
![[Pasted image 20230602153551.png]]

Statistics
![[Pasted image 20230602153808.png]]

Selection cardinality

> [!NOTE] 
> The formula is true only for uniform data. In real world the data is not uniform.

![[Pasted image 20230602153939.png]]

Complex Predicates
Selectivity (sel)
![[Pasted image 20230602154207.png]]

Selection - Complex Predicates
(Assuming uniform data)
![[Pasted image 20230602154452.png]]

Selections - Complex Predicates
Range Predicate: (WRONG)
![[Pasted image 20230602154644.png]]

Selections - Complex Predicates
Negation Query:
![[Pasted image 20230602154733.png]]

Selections - Complex Predicates
Conjunction
![[Pasted image 20230602155054.png]]

Selections - Complex Predicates
Disjunction
![[Pasted image 20230602155119.png]]

Slection Cardinality:
3 Assumption
1. Uniform Data
2. Independent Predicates
3. Inclusion Principle
![[Pasted image 20230602155423.png]]

Correlated Attributes
![[Pasted image 20230602155700.png]]

Cost Estimations
In real life data isn't uniform so we need to store for each column the number of tuple in each row.
This is also too much so be divided the rows in buckets.
![[Pasted image 20230602160010.png]]

Bucket Ranges
![[Pasted image 20230602160159.png]]

Histograms with Quantiles
![[Pasted image 20230602160321.png]]

![[Pasted image 20230602160405.png]]

Sampling
We collect a small part of a big table to estimate selectivity.
![[Pasted image 20230602160647.png]]

Query Optimization
![[Pasted image 20230602160934.png]]

Single-Relation Query Planning
![[Pasted image 20230602161146.png]]

OLTP Query Planning
Query planning for OLTP queries is easy because they are sargable (Seach Argument Able)
![[Pasted image 20230602161520.png]]

Multi-Relation Query Planning
![[Pasted image 20230603155720.png]]

Multi-Relation Query Planning
System R (IBM DB) only consider left-deeep join trees 
![[Pasted image 20230603155813.png]]

Multi-Relation Query Planning
![[Pasted image 20230603160046.png]]

Candidate Plan Example
![[Pasted image 20230603160326.png]]

Candidate Plans
Step 1
![[Pasted image 20230603160445.png]]

Candidate Plans
Step 2
![[Pasted image 20230603160515.png]]

Candidate Plans
Step 3
![[Pasted image 20230603160552.png]]

Postgres Optimizer
![[Pasted image 20230603160832.png]]

Nested Sub-Queries
![[Pasted image 20230603161144.png]]

Nested Sub-Queries - Approach 1: Rewrite 
![[Pasted image 20230603161250.png]]

Nested Sub-Queries - Approach 2: Decompose 
![[Pasted image 20230603161349.png]]
![[Pasted image 20230603161424.png]]

## 16 - Concurrency Control Theory

![[Pasted image 20230603162540.png]]

Concurrency Control & Recovery
ACID
![[Pasted image 20230603162610.png]]

Transaction in SQL
txn starts with BEGIN command
txn stops with either COMMIT or ABORT
![[Pasted image 20230603164056.png]]

ACID (Atomicity, Consistency, Isolation, Durability)
![[Pasted image 20230603164257.png]]

Atomic
![[Pasted image 20230603184349.png]]

Mechanisms for Ensuring Atomicty
1. Logging
![[Pasted image 20230603184517.png]]

2. Shadow Paging
![[Pasted image 20230603184719.png]]

Consistency
![[Pasted image 20230603185051.png]]

Isolation 
![[Pasted image 20230603185419.png]]

Isolation
Concurrency Control
![[Pasted image 20230603185443.png]]

Isolation
Conflict Serializable Schedules
![[Pasted image 20230603190733.png]]
![[Pasted image 20230603190810.png]]

Isolation
Serializability
![[Pasted image 20230603190842.png]]

Isolation
Dependency graph (DAG)
![[Pasted image 20230603190949.png]]

## 17 - Two-Phase Locking Concurrency Control

Lock
![[Pasted image 20230603192120.png]]

![[Pasted image 20230603192244.png]]

Lock Types
1. S-Lock - Shared locks for reads
2. X-Lock - Exclusive locks for writes
![[Pasted image 20230603192711.png]]


Concurrency Control Protocol
Two-phase Locking (2PL)
![[Pasted image 20230603193031.png]]

Two-phase Locking
Phase 1: Growing
Phase 2: Shrinking
![[Pasted image 20230603193202.png]]

![[Pasted image 20230603193318.png]]

![[Pasted image 20230603193424.png]]

Cascading aborts
![[Pasted image 20230603193559.png]]

2PL - Cascading Aborts
![[Pasted image 20230603193719.png]]

2PL - Observations
![[Pasted image 20230603193821.png]]


Strict Two-Phase Locking
![[Pasted image 20230603193919.png]]
![[Pasted image 20230603194041.png]]


Universe of Schedules
![[Pasted image 20230603194509.png]]

2PL Deadlocks
![[Pasted image 20230603194604.png]]

Approch 1: Deadlock Detection (waits for graph)
![[Pasted image 20230603194647.png]]

Deadlock Handling
![[Pasted image 20230603195143.png]]

Deadlock Handling: Victim Selection
![[Pasted image 20230603195238.png]]

Deadlock Handling:  Rollback length
![[Pasted image 20230603195345.png]]

Approch 2: Deadlock Prevention
![[Pasted image 20230603200213.png]]

![[Pasted image 20230603200320.png]]

![[Pasted image 20230603200522.png]]

Lock Granularities
![[Pasted image 20230603200622.png]]

Database Lock Hierarchy
![[Pasted image 20230603200730.png]]

Intention Locks
![[Pasted image 20230603200929.png]]
![[Pasted image 20230603201020.png]]
![[Pasted image 20230603201038.png]]
![[Pasted image 20230603201057.png]]

Multiple Lock Granularities
![[Pasted image 20230603201455.png]]

## 18 - Timestamp Ordering Concurrency Control

Concurrency Control Approaches
2PL -> Pessimistic protocol
Timestamp Ordering (T/O) -> Optimistic
![[Pasted image 20230604221607.png]]

T/O Concurrency Control
![[Pasted image 20230604221747.png]]

Timestamp Allocation
![[Pasted image 20230604221913.png]]

Basic T/O
![[Pasted image 20230604222422.png]]

Basic T/O - Reads
![[Pasted image 20230604222540.png]]

Basic T/O - Writes
![[Pasted image 20230604222759.png]]

Thomas Write Rule
![[Pasted image 20230604223624.png]]

Basic T/O
![[Pasted image 20230604223814.png]]

Recoverable Schedules
![[Pasted image 20230604223922.png]]

Basic T/O - Performance Issues
![[Pasted image 20230604224211.png]]


![[Pasted image 20230604224422.png]]

Optimistic Concurrency Control (OCC)
![[Pasted image 20230604224531.png]]

OCC Phases
![[Pasted image 20230604224623.png]]

OCC - Validation Phase
![[Pasted image 20230604224911.png]]

OCC - Serial Validation
![[Pasted image 20230604225031.png]]

OCC - Observations
![[Pasted image 20230604225956.png]]

OCC - Perfomance Issues
![[Pasted image 20230604230121.png]]

Parititio-Based T/O (horizontal partitions aka shards)
![[Pasted image 20230604230233.png]]

Horizontal Partitioning
![[Pasted image 20230604230633.png]]

Partition-Based T/O
![[Pasted image 20230604230947.png]]

Partition-Based T/O - Reads
![[Pasted image 20230604231054.png]]

Partition-Based T/O - Writes
![[Pasted image 20230604231122.png]]

Partition-Based T/O - Performance Issues
![[Pasted image 20230604231329.png]]

The Phantom problem
![[Pasted image 20230604231626.png]]
![[Pasted image 20230604231710.png]]

Predicate Locking
Hard to implement -> Nobody do it
![[Pasted image 20230604231724.png]]

Index Locking
![[Pasted image 20230604231825.png]]

Locking without an Index
![[Pasted image 20230604231944.png]]

Repeating Scans
![[Pasted image 20230604232045.png]]

Weaker Levels of Isolation
![[Pasted image 20230604232229.png]]

Isolation Levels
![[Pasted image 20230604232306.png]]
![[Pasted image 20230604232414.png]]
![[Pasted image 20230604232443.png]]
![[Pasted image 20230604232510.png]]
![[Pasted image 20230604232559.png]]

Access Modes
![[Pasted image 20230604232749.png]]

## 19 - Multi-Version Concurrency Control

Multi-version Concurrency Control
![[Pasted image 20230608163413.png]]

MVCC History
![[Pasted image 20230608163625.png]]

Multi-version Concurrency Control 
snapshot
time-travel
![[Pasted image 20230608163838.png]]

Concurrency Control Protocol
1. Timestamp Ordering
2. Optimistic Concurrency Control
3. Two-Phase Locking
![[Pasted image 20230608171243.png]]
## 20 - Database Logging Schemes

## 21 - ARIES Database Recovery

## 22 - Introduction to Distributed Databases

## 23 - Distributed OLTP Databases

## 24 - Distributed OLAP Databases

## 25 - Shasank Chavan (Oracle In-Memory Databases)

## 26 - Systems Potpourri



