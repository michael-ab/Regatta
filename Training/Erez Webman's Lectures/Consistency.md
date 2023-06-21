[Erez Webman - Consistency](https://drive.google.com/drive/u/0/folders/19CbACTV4c2beowEvOGm0z8gwj8oCnfmh "https://drive.google.com/drive/u/0/folders/19CbACTV4c2beowEvOGm0z8gwj8oCnfmh")

### Conflict Serializable

Conflict Serializable iff no circle in the dependencies graph
Example:
![[Conflict Serializable]]

Conflicts:
1. R/W
2. W/R
3. W/W

### 2PL 
Nobody use the 2PL as is but strict 2PL or SS2LP

![[Strict 2PL]]

### Recoverability

Not recoverable transaction example:
![[Not recoverable txn example]]

### ACA
(Avoids cascading aborts)

• Avoids cascading aborts (ACA)
If T_i reads x from T_j , then commit_j< read_i(x)

See [[DMS-HS20-Transactions_CCR.pdf]]

![[Pasted image 20230620183847.png]]


### MVCC

- Snapshot creation
- Snapshot read
- Isolated writes
- Read-after-Writes
- Commitment

![[MVCC]]

Snapshot delete/ Reclamation -> Need to be efficient and "just on time"
