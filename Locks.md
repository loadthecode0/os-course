## Lock variables
- lock is a shared variable
- ![[Pasted image 20241207213944.png]]
- The code is not safe from race conditions because the `if (lock == 0)` check and `lock = 1` update are not atomic. This can lead to multiple threads entering the critical region simultaneously. To fix this, use atomic instructions, mutexes, or semaphores to ensure proper synchronization and mutual exclusion.
### Example
![[Pasted image 20241207214125.png]]
![[Pasted image 20241207214138.png]]
output
![[Pasted image 20241207214508.png]]
- Same behaviour as before!
- 'lock' is like a normal shared variable -> subject to race conditions when used like this.
- solution -> [[Strict Alternation]] -> *but not the IDEAL solution!*
