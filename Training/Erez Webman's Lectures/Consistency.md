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


### OR2MW (Other Reads to My Writes)
Regatta Algo
Waitable (can wait) if the is some colisions
When a txn TX* finish, we compare the write vector W(x1, x2, ..., xn) with the read vector Ri(x1, x2, ..., xn) of all active txns.
For i in all ID of all active txns
	if W(x1, x2, ..., xn) intersection Ri(x1, x2, ..., xn) -> Not empty
		Abort TX*

### MR2OW
See TP Consistency #14 - Manipulation to understand why:
No need for MR2OW
No need for snapshots

