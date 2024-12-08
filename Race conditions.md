- the situation where the **outcome** depends on the **timing** of process/thread execution (scheduling)
- *Scheduling is effectively random* (unpredictable and uncontrollable) from the POV of process/thread.
- A race condition leads to unexpected **non-deterministic** behaviour
	- *Bugs that appear rarely and are hard to explain*
	- *Plain testing not sufficient*

## Avoiding Race Conditions
### Identify Critical Regions
- **critical regions:** the part of the programme where the shared memory, shared file, or other shared resource is accessed.
### Mutual Exclusion
- **Locking and unlocking of resources:** Ensure that only one process/thread can enter the critical region.
- public toilet example
![[Pasted image 20241207213729.png]]
### Cost of mutual exclusion
- prevents full parallelization -> try to make critical regions as small as possible

## [[Locks]]
