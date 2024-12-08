- *each process has a virtual address space*
	- we call them **virtual addresses**
- Address space is split into chunks that we call **pages**
	- each page is a continuous range of addresses.
- Not all pages need to be in physical memory for a process to run
	- all pages are stored in the **hard drive**
- If a programme accesses an address 
	- that is in memory -> all good
	- that is NOT in memory -> **Page Fault**
		- OS takes control, fetches the missing piece, instruction is executed again.

## Memory Management Unit
- CPU contains hardware that *maps virtual addresses to the physical address.*
![[Pasted image 20241208120422.png]]
- *transfers bw memory and disk are always in whole pages*
	- even if one single variable

## Paging example
![[Pasted image 20241208120614.png]]
- understood the formula!
- **Disadvantage:** math is not quick for machines
	- use [[#Page Tables]]
## Page Tables
![[Pasted image 20241208121128.png]]
- efficient to implement and faster
### Large Page Tables
- Multiple tiers
- ![[Pasted image 20241208121347.png]]

## [[Page Replacement Algorithms]]
