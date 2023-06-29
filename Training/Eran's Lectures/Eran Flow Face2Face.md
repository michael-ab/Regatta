Several sort of queries:
1. DDL (Data Definition Language) -> 
2. DML (Data Manipulation Language) -> INSERT, SELECT, UPDATE, and DELETE commands
3. DQL
4. (SHOW)
![[Pasted image 20230629180714.png]]
RDB module
Only 1 in the system:
1. Sequencer
2. GDB (Global Deadlock Detector)
3. SPM/DCM

Client  N <-> N Cluster
Drivers on top of client

client manager send command to client agents

client manager (Naama) is on CLI

client agents is on RDB

client agents chose a Transaction manager in one of the node


RDB                                                                                DCM
NORTH
Client Agents                                                  DCM / SMM / SAM
Transaction Manager
Statement Processor
Parser
Builder DCA (DDL and show stop here to the DCM)
static optimizer
dynamic optimizer
Exec Builder / Planner / Execution Mgr (same thing) (Ben and Yuval)
Output/Data Collector
-----------------------//
SOUTH
Exec Agent (Ben and Yuval)
Transaction Agent (Naama)
Operator Pipe (Output/Data Collector) (Hilla, Amit, Eran G.)
Consistency (Barak, Nitsan)
------------------------//
NSM/SPA (Alex)
DataStore/IndexStore (Alon, Roy, Sari, etc.) (row store for now later maybe also column store)
B-Tree (R2P) (Michael)
LSA (Roy)
----------------------//
Ranger (Eddy) (1 per module today/ maybe 1 per device in the future)


CORE (Eran)
NET (Alone & Ariel K.)


















