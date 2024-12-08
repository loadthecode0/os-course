- **Source of problem:**
	- process can be pre-empted *between the instruction that checks the lock variable and the instruction that sets the lock variable*. 
	- so, it would help if the checking and setting would be **indivisible** or **atomic**

## Disabling interrupts
- no clock interrupts => no preemption => no race conditions
- **Problems**
	- allowing users to disable interrupts can be catastrophic
	- [!] can implement *locks at the kernel* (?) -> Contiki-NG OS
	- works only in **single processor systems**
- Pseudocode:
```c
while (1)
{
	disable_interrupts();
	critical_regions();
	enable_interrupts();
}
```

## Atomic Instructions
![[Pasted image 20241207233226.png]]

## Spinlock and busy waiting
![[Pasted image 20241207233442.png]]

## [[Mutex]]
