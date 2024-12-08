- lets the running process to run until it **blocks** or until it **exits** or until it **voluntarily releases** the CPU.
- *Cooperative Scheduling* (alternative name)
- Advantages -> avoids a lot of context switches, overheads
- Disadvantages -> control issues
	- can't be used in multi-user systems
- useful in specialised embedded systems 

- Examples:
	- [[#First Come, First Served (FIFO)]]
	- [[#Shortest Job First]]
	- [[#Round Robin Scheduling]]
## First Come, First Served (FCFS)
- Principle -> CPU given to the processes in the order they request it.
- Simple implementation:
	- All ready processes in FIFO
	- The scheduler selects a process at the beginning of the queue
	- When a process becomes ready, it goes at the end of the queue
- Disadvantages:
	- short jobs wait for long jobs -> lead to high average latency

## Shortest Job First
- Principle -> the scheduler selects the shortest process first
- Minimises the mean turnaround time
- Disadvantages:
	- It's hard to know running times beforehand. Maybe input dependent.

## Round Robin Scheduling
- principle -> each process is allowed to run for up to some fixed time.
- ![[Pasted image 20241205171615.png]]
- *How long should a time quantum be?*
	- **Efficiency vs Delay trade off**:
		- Context Switch takes time
		- very short quantum results to high overhead
		- very long quantum results to high response time
	- Typically 20-50 ms is a reasonable compromise.