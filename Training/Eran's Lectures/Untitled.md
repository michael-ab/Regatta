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


RDB
Client Agents
Transaction Manager
Statement Processor
Parser
Builder DCA
static optimizer
dynamic optimizer
Exec Builder / Planner / Executio






