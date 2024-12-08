- *Only one process can be at a running state per CPU*
- Multiple processes in the ready state **compete** for the CPU.
	- The decision is up to the scheduler.
## Scheduler
- decides which process 
	- (parent or child) to run after a fork
	- to run after the running process calls exit
	- to run when a process gets blocked waiting for I/O
	- to run when a process gets unblocked (i.e ready)

## Forcing a running process to stop
- scheduler must use the CPU to make decisions.
- *The CPU is available after a fork, exit, or when a process blocks.*
- [?] How can the scheduler get the CPU from a running process?
	- can't be done at software level
	- done at hardware level -> **Interrupts** -> major factor for classifying 
# Scheduling Algorithms
No one scheduling algorithm which can be good for every case.
## [[Pre-emptive Scheduling]]

## [[Non-pre-emptive Scheduling]]

## Priorities
- **High Priority Processes**
	- ![[Pasted image 20241205171924.png]]
	- [!] I/O bound processes are high priority
		- spend majority of time waiting for responses from devices
		- the I/O related operations and CPU based operations can be parallelized -> which can reduce idle time.
- **Low Priority Processes**
	- eg downloading
### Priority based Scheduling
- Principle -> Each process gets a priority number
- Scheduler selects the process with the highest priority
- ![[Pasted image 20241205172440.png]]
- Dynamic priority levels
#### priority groups
![[Pasted image 20241205172606.png]]

## Lottery Scheduling
- next process is selected randomly
- cooperative processes may exchange tickets

## fair share Scheduling
- processes have owners
- in multi-user environments, we want fairness at user level.

