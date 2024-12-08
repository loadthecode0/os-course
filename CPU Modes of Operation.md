## Kernel Mode
- CPU can **execute every instruction** and **use all hardware**.
- OS runs in Kernel mode typically.

## User Mode
- Allowed instructions and hardware resources are limited.
- All *user programs run in user mode*.
- accessing protected resources ->
	- make **system calls** -> **trap** -> normal execution is suspended and OS takes control.
![[Pasted image 20241123190608.png]]

## Why have different modes?
- why not do everything in kernel mode?
- enforce management policies
- stability thru isolation -> a bug in user mode can't take down the entire system
- security in multi user systems

- However user mode is costly
	- transition bw kernel/user modes is expensive

## How to decide which service to run in kernel or in user mode?
- **Stability vs Efficiency trade-off**
- *4 types*
#### Monolithic Systems:
- entire OS runs as a single program in kernel mode -> user programs access OS services via system calls.
- Advantages ->
	- v efficient
- Disadvantages -> 
	- A bug in one OS service can take down the entire system
	- less flexible
		- any system extensions require rebuilding the kernel
- E.g Linux
#### Layered Systems
- hierarchy of layers
- ![[Pasted image 20241123191409.png]]
- Advantages ->
	- High flexibility
		- easy to extend as long as we adhere to the interface with layer above and below
- Disadvantages ->
	- Low efficiency
		- A procedure in an outer layer must make the equivalent of multiple system calls to access inner resources
	- Defining layers is not straightforward.

#### Microkernels
- v small kernel
	- basic management protocols
- run all non essential services of the OS in user mode
	- communication bw them w message passing
- Advantages ->
	- high stability
	- high flexibility
- Disadvantages -> 
	- high overhead from message passing

![[Pasted image 20241123191812.png]]


#### Hybrid systems
![[Pasted image 20241123191935.png]]
