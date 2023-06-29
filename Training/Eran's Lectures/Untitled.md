DDL 
DML
DQL
SHOW
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
Client Agents
Transaction Manager
Statement Processor
Parser
Builder DCA (DDL and show stop here to the DCM)
static optimizer
dynamic optimizer
Exec Builder / Planner / Execution Mgr (same thing) (Ben and Yuval)
-----------------------//
SOUTH
Exec Agent (Ben and Yuval)
Transaction Agent (Naama)
Operator (Hilla, Amit, Eran G.)
Consistency (Barak, Nitsan)










