- second layer of parallelism
- traditionally-> each process -> 1 thread of control
- multihreading -> each process -> multiple threads
- **Different to processes**
	- threads share same address space (processes share same address space)
	- threads are more lightweight
		- faster context switching, good hardware support
		- faster creation and termination
	- **Advantages of processes over threads**
		- processes offer isolation
			- programming w threads -> more challenging and complex
				- need for [[Thread Synchronization]]
			- No protection on shared resources
				-  thread can read/write or even erase the stack of another
				- a bug in one thread an take the whole process down.
			- *Chrome uses one process per tab*
				- allows to sacrifice only that tab if it crashes
- *Threads can be implemented either at user or kernel level*
- 
## Sharing of resources
![[Pasted image 20241206133328.png]]

## [[POSIX Threads]]

## Applications
![[Pasted image 20241206133821.png]]
![[Pasted image 20241206133910.png]]

## [[Thread Scheduling]]


## Class example
### 1: Process forking
![[Pasted image 20241206135721.png]]
output
![[Pasted image 20241206135730.png]]
They both get a copy of the address space, so each pointer is independent. No memory sharing, processes don't share global variables in heap memory.

### 2: Threading
![[Pasted image 20241206140216.png]]
output
![[Pasted image 20241206140248.png]]
Same address space.
Also if we run it for a long number of times, we may get 51 51, when scheduler interrupts the thread to execute the other.

