Carnegie Mellon University database systems course

All DBs:
https://dbdb.io/

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
2. Each attribute is embedded with the tuple IDs
![[Pasted image 20230519152725.png]]

Pro/cons DSM
![[Pasted image 20230519152935.png]]

## 05 - Buffer Pool - Memory Management

> [!NOTE] Title
> Memory part (not disk!)

Dirty flag: a bit to know if the page was modified 
Pin/Reference Counter: number of threads/queries correctly running that want this page in memory
![[Pasted image 20230519165553.png]]

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

### Sorting Algo

Issue for disk: we need to find a good sorting algo that don't do write too much data out the disk
![[Pasted image 20230529213842.png]]

External Merge Sort
![[Pasted image 20230529213856.png]]

2-Way External Merge Sort
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
inner equijoin algorithms
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

Probe Phase Optimization
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

Heap Clustering (clustering index)
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
total cost of ownership (TCO)
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
Serial
Conflict Serializable
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


Isolation Levels
1. Serializable
2. Repeatable Reads
3. Read Committed
4. Read Uncommitted
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
Snapshot
Time-travel
![[Pasted image 20230608163838.png]]

Concurrency Control Protocol
1. Timestamp Ordering
2. Optimistic Concurrency Control
3. Two-Phase Locking
![[Pasted image 20230608171243.png]]

Version Storage
version chain
![[Pasted image 20230608172846.png]]

Version Storage
1. Append-Only Storage
2. Time-Travel Storage
3. Delta Storage
![[Pasted image 20230608172941.png]]

Append-ONLY Storage
![[Pasted image 20230608173156.png]]

Version Chain Ordering
1. Oldest-to-Newest (O2N)
2. Newest-to-Oldest (N2O)
![[Pasted image 20230608173311.png]]

Time-Travel Storage
![[Pasted image 20230608173524.png]]

Delta Storage
![[Pasted image 20230608173744.png]]

Garbage Collection
![[Pasted image 20230608173815.png]]

Garbage Collection
1. Tuple-Level
2. Transaction-Level
![[Pasted image 20230608173914.png]]

Tuple-Level GC
(Dirty page BitMap)
![[Pasted image 20230608174137.png]]

Cooperative Cleaning
![[Pasted image 20230608174414.png]]

Index Management
![[Pasted image 20230608174503.png]]

Secondary Indexes
1. Logical Pointers
2. Physical Pointers
![[Pasted image 20230608174539.png]]

## 20 - Database Logging Schemes

Crash Recovery
![[Pasted image 20230608175230.png]]

Crash Recovery
![[Pasted image 20230608175412.png]]

Failure Classification
1. Transaction Failures
2. System Failures
3. Storage Media Failures
![[Pasted image 20230608175509.png]]

Transaction Failures
![[Pasted image 20230608175605.png]]

System Failures
![[Pasted image 20230608175700.png]]

Storage Media Failure
![[Pasted image 20230608180306.png]]

Undo vs Redo
![[Pasted image 20230608181643.png]]

Buffer Pool
![[Pasted image 20230608181851.png]]

Steal Policy
steal=voler
When a txn need more space in the buffer pool, can we allow the eviction of uncomitted txn to the disk to have more space for the first txn?
![[Pasted image 20230608182009.png]]

Force Policy
![[Pasted image 20230608182050.png]]

No-Steal + Force
![[Pasted image 20230608182203.png]]
![[Pasted image 20230608182513.png]]

Shadow Paging
![[Pasted image 20230608182601.png]]
![[Pasted image 20230608182709.png]]

Shadow Paging - Disadvantages
![[Pasted image 20230608183121.png]]

Write-Ahead Log
![[Pasted image 20230608183340.png]]

Wal Protocol
![[Pasted image 20230608183510.png]]
![[Pasted image 20230608183537.png]]
![[Pasted image 20230608183622.png]]
![[Pasted image 20230608183819.png]]
![[Pasted image 20230608184029.png]]

Buffer Pool Policies
![[Pasted image 20230608184501.png]]

Logging Schemes
![[Pasted image 20230608184640.png]]

Physical vs Logical Logging
![[Pasted image 20230608184732.png]]

Physiological Logging
![[Pasted image 20230608184835.png]]

Logging Schemes
![[Pasted image 20230608184953.png]]

Checkpoints
![[Pasted image 20230608185117.png]]
![[Pasted image 20230608185206.png]]
![[Pasted image 20230608185331.png]]
![[Pasted image 20230608185401.png]]

Checkpoints - Frequency
![[Pasted image 20230608185438.png]]

## 21 - ARIES Database Recovery

Crash Recovery
![[Pasted image 20230611185813.png]]

ARIES
![[Pasted image 20230611185847.png]]

ARIES
![[Pasted image 20230611190127.png]]

WAL Records
Log Sequence Number (LSN)
![[Pasted image 20230611190511.png]]

Log Sequence Numbers
FlushedLSN 
PageLSN 
RecLSN 
LastLSN 
MasterRecord
![[Pasted image 20230613192412.png]]

Writing Log Records
![[Pasted image 20230613192531.png]]

Writing Log Records
![[Pasted image 20230613192832.png]]

Writing Log Records
![[Pasted image 20230613193301.png]]

Transaction Commit
![[Pasted image 20230613193540.png]]

Transaction Abort
![[Pasted image 20230613193733.png]]

Compensation Log Records (CLR)
![[Pasted image 20230613194102.png]]

Abort Algorithm
![[Pasted image 20230613201050.png]]

Non-Fuzzy Checkpoints
![[Pasted image 20230613201249.png]]
![[Pasted image 20230613201329.png]]
![[Pasted image 20230613201624.png]]

Active Transaction Table
![[Pasted image 20230613201800.png]]

Dirty Page Table
![[Pasted image 20230613201857.png]]

Fuzzy Checkpoints
![[Pasted image 20230613202033.png]]

Fuzzy Checkpoints
![[Pasted image 20230613202203.png]]

ARIES - Recovery Phases
1. Analysis
2. Redo
3. Undo
![[Pasted image 20230613202333.png]]

ARIES - Overview
![[Pasted image 20230613202600.png]]

Analysis Phase
![[Pasted image 20230613202642.png]]

Analysis Phase
ATT
DPT
![[Pasted image 20230613202806.png]]

Redo Phase
![[Pasted image 20230613203232.png]]

Redo Phase
![[Pasted image 20230613205021.png]]
![[Pasted image 20230613205116.png]]

Undo Phase
![[Pasted image 20230613205151.png]]

Additional Crash Issues (1)
![[Pasted image 20230613205540.png]]

Additional Crash Issues (2)
![[Pasted image 20230613205641.png]]

## 22 - Introduction to Distributed Databases

System Architecture
1. Shared Everything
2. Shared Memory
3. Shared Disk
4. Shared Nothing
![[Pasted image 20230614210644.png]]

Shared Memory
![[Pasted image 20230614210728.png]]

Shared Disk
![[Pasted image 20230614211218.png]]

Shared Nothing
![[Pasted image 20230614213312.png]]
![[Pasted image 20230614213620.png]]

Homogenous vs Heterogenous
![[Pasted image 20230614214719.png]]

MongoDB Heterogenous Architecture
![[Pasted image 20230614214904.png]]

Data Transparency
![[Pasted image 20230614215023.png]]

Database Partitioning
![[Pasted image 20230614215140.png]]

Naïve Table Partitioning
![[Pasted image 20230614215405.png]]

Horizontal Partitioning
![[Pasted image 20230614215525.png]]
![[Pasted image 20230614215617.png]]

Consistent Hashing
![[Pasted image 20230616125610.png]]

Consistent Hashing
![[Pasted image 20230616125753.png]]

Consistent Hashing
Replication Factor=3
![[Pasted image 20230616125836.png]]

Logical Partitioning
![[Pasted image 20230616130114.png]]

Physical Partitioning
![[Pasted image 20230616130146.png]]

Single-Node vs Distributed
![[Pasted image 20230616130220.png]]

Transaction Coordination
Centralized
Decentralized
![[Pasted image 20230616130345.png]]

TP Monitors
Example of centralized coordinator
![[Pasted image 20230616130458.png]]

Centralized Coordinator 
![[Pasted image 20230616130628.png]]
![[Pasted image 20230616130712.png]]

Centralized Coordinator
Another example with middleware
![[Pasted image 20230616130859.png]]

Decentralized Coordinator
![[Pasted image 20230616131035.png]]

Distributed 2PL
![[Pasted image 20230616131234.png]]

## 23 - Distributed OLTP Databases

OLTP vs OLAP
![[Pasted image 20230616152006.png]]

Byzantine Fault Tolerant Protocol for txns (blockchain)
![[Pasted image 20230616152453.png]]

Atomic Commit Protocol
![[Pasted image 20230616152746.png]]

Two-Phase Commit (Success)
Coordinator
Participant
![[Pasted image 20230616153318.png]]

Two-Phase Commit (Abort)
![[Pasted image 20230616153451.png]]

2PC Optimizations
1. Early Prepare Voting
2. Early Acknowledgement After Prepare
![[Pasted image 20230616153828.png]]

Early Acknowledgement 
![[Pasted image 20230616154313.png]]

Two-Phase Commit
![[Pasted image 20230616154707.png]]

Paxos
![[Pasted image 20230616154751.png]]

Paxos
![[Pasted image 20230616155121.png]]

Paxos
Example:
![[Pasted image 20230616155239.png]]

Multi-Paxos
![[Pasted image 20230616155415.png]]

2PC vs Paxos
![[Pasted image 20230616155705.png]]

Replication
![[Pasted image 20230616155907.png]]

Replica Configurations
1. Master-Replica
2. Multi-Master
![[Pasted image 20230616160013.png]]

1. Master-Replica
2. Multi-Master
![[Pasted image 20230616160436.png]]

K-Safety
threshold
![[Pasted image 20230616160848.png]]

Propagation Scheme
Propagation Levels:
- Synchronous (Strong Consistency)
- Asynchronous (Eventual Consistency)
![[Pasted image 20230616161014.png]]

Propagation Scheme
1. Synchronous
2. Asynchronous
![[Pasted image 20230616161322.png]]

Propagation Timing
1. Continuous
2. On commit
![[Pasted image 20230616161550.png]]

Active vs Passive
![[Pasted image 20230616161733.png]]

CAP Theorem
![[Pasted image 20230616162110.png]]

CAP Theorem
![[Pasted image 20230616162200.png]]

CAP - Consistency
![[Pasted image 20230616162314.png]]

CAP - Availability
![[Pasted image 20230616162356.png]]

CAP - Partition Tolerance
![[Pasted image 20230616162548.png]]

CAP for OLTP DBMs
![[Pasted image 20230616162732.png]]

Federated Databases
![[Pasted image 20230616162938.png]]

Federated Databases Example
![[Pasted image 20230616163117.png]]

## 24 - Distributed OLAP Databases

Bifurcated Environment
![[Pasted image 20230616163729.png]]

Decision Support Systems
Star Schema vs Snowflake Schema
![[Pasted image 20230616163936.png]]

Star Schema
![[Pasted image 20230616164231.png]]

Snowflake Schema
![[Pasted image 20230616164422.png]]

Star vs Snowflake Schema
Issues:
1. Normalization
2. Query Complexity
![[Pasted image 20230616164456.png]]

Push vs Pull
![[Pasted image 20230616164950.png]]

Push Query to Data
![[Pasted image 20230616165240.png]]

Pull Data to Query
![[Pasted image 20230616165517.png]]

Query Fault Tolerance
![[Pasted image 20230616165835.png]]

Query Planning
![[Pasted image 20230616170136.png]]

Query Plan Fragments
1. Physical Operators
2. SQL
![[Pasted image 20230616170303.png]]

Query Plan Fragments (approch 2 - SQL)
![[Pasted image 20230616170546.png]]

Distributed Join Algorithms
![[Pasted image 20230616170832.png]]

Semi-Join
![[Pasted image 20230616174208.png]]

Relational Algebra: Semi-Join
![[Pasted image 20230616174500.png]]

Cloud Systems
database-as-a-service DBaaS
![[Pasted image 20230616174544.png]]

Cloud Systems
1. Managed DBMS
2. Cloud-Native DBMS
![[Pasted image 20230616175017.png]]

Serverless Databases
![[Pasted image 20230616175300.png]]

Disaggregated Components
![[Pasted image 20230616175556.png]]

Universal Formats
![[Pasted image 20230616175801.png]]
![[Pasted image 20230616175934.png]]

## 25 - Shasank Chavan (Oracle In-Memory Databases)

- Oracle innovations
Intel Optane
![[Pasted image 20230617151809.png]]

## 26 - Systems Potpourri
Scuba
MongoDB
CockroachDB

