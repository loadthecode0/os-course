## Example 2
![[Pasted image 20241207235447.png]]
- **Risk for deadlock**
- A waits for B while B waits for A
	- e.g sendmoney(0,1,100) in parallel with sendmoney(1,0,200)
- *To avoid deadlocks, we must lock resources always in the same order.*
	- instead of unlocking sender account first, lock the account with smaller account number first.

