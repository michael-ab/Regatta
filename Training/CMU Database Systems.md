Carnegie Mellon University databse systems course

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
Dirty flag: a bit t