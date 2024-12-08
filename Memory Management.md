## Memory Abstraction
### Example 1
![[Pasted image 20241208110131.png]]
output:
![[Pasted image 20241208112857.png]]
- [?] If they have the same address for A, why is the increment to different variables?
	- These ARE two different variables
	- But *memory abstraction by OS* -> these addresses are virtual memory addresses
		- same virtual addresses but different physical addresses!

## What happens without memory abstraction?
![[Pasted image 20241208112944.png]]
- challenging to have two processes running which both access the same memory.
- no sufficient protection - can access the OS in the RAM by mistake
### Memory Protection Keys
![[Pasted image 20241208113242.png]]
- **Problem:**
	- shifting memory - will not consider the hardcoded physical memory address in he instrutions
	- here, jmp 28 will cause the program to jump to actual location 28
	- calls for *static relocation* - add the shift to every instruction
		- static -> compile time or load time
## Relocation
- process of mapping a program’s logical addresses (used in the program code) to physical addresses in memory. 
- *necessary because* programs typically don’t know in advance where they will be loaded in memory. 
- can either be **static** or **dynamic**, depending on when and how the mapping is performed.

## Memory Abstraction
- programmes don't directly see the physical memory
	- see only their address space
- **Address space:**
	- the set of addresses a process can use
	- MOV REG1, 1000 - corresponds to address 1000 within the address space
	- ![[Pasted image 20241208113825.png]]

## Dynamic Relocation
- **base** and **limit** registers
- every time a process references a memory address, the *CPU adds the base value to the address* before talking to the RAM.
- For *protection*, it checks if address is less than the limit value.
- **DIsadvantage:** extra addition and comparison overhead with every memory reference
- ![[Pasted image 20241208114131.png]]

## Memory Overload
- can load multiple processes in memory
- there may not be enough RAM to keep all running processes in memory.
- **Swapping:**
	- temporarily moving a process or part of a process from **RAM** to a **swap space** (on disk) to free up memory for other processes.
	- ![[Pasted image 20241208114622.png]]
	- OS systems got faster when we shifted from magnetic disks to solid state drive.
	- **notice process A:** base/limit registers need to be readjusted to a new location.
	- *How swapping works*:
		- When the system runs out of **physical memory (RAM),** the OS identifies a process (or parts of a process) that is idle or least used and swaps it out to disk.
		- The freed-up RAM is then allocated to the active process that requires memory.
		- If the swapped-out process becomes active or its data is needed again, the OS swaps it back into RAM, possibly swapping out another process to make space.
	- *Swap space:*
		- dedicated area on disk (**swap space**), used to store the swapped-out process data.
		- can be a separate partition or a file on the disk.
	- *Use of bitmapping to manage free memory*
		- ![[Pasted image 20241208115544.png]]
		- v slow
	- *Use of DLL to manage free memory*
		- ![[Pasted image 20241208115658.png]]
		- linked list of allocated and free segments
		- advantages - easy to maintain, faster
		- different allocation strategies - try to not leave small holes.
## Challenge
- memories increase rapidly, but *software sizes increase much faster*.
- [?] How to run a programme that is too large to fit in memory?
- need to use [[Virtual Memory]]

## [[Virtual Memory]]

## [[Virtual Memory#Memory Management Unit|Memory Management Unit]]

