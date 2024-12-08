- **Sequential process:**
	- an abstraction for executing a program
	- CPU is shared among multiple processes that run in parallel.
		- **Pseudoparallel** if the system has only one CPU
		- The CPU is managed by the [[Process Scheduling|scheduler]].
	- **[[#Context switch]]** -> the scheduler switches the processes.
		- Each process has its **logical PC** and its own **virtual CPU**
	- ![[Pasted image 20241205161601.png]]
- `ps -ef`: process status, e for all, f for full format
	- display list of all processes running on the system
## Context Switch

- [?] If I run my text editor 10 times, to edit 10 different files, how many processes do I get?
	- 10 or more
- 