- [[The process model]]
- [[Process Creation]]
- [[Process Termination]]
- [[Process Table#Process states | Process States]]
- [[Process Behaviours]]
- Process [[Process Scheduling]]
- A program in execution
- associated with it address space
- other resources (e.g registers, open files)
- **A process is a container that holds all the info needed to execute a program.**
	- From a process's POV, all memory is available to it (this is an abstraction).
- Multiprogramming env -> multiple processes run in *parallel* or *pseudo-parallel*.
	- pseudo-parallel -> very fast switching that it looks parallel
- OS maintains **[[Process Table]]** -> list of all processes (active, suspended, terminated until reaped).
	- Each process has a unique *Process ID* (PID) and an *owner*
		- [?] Owner?
- processes **operate in user mode** -> restricted privileges
- *processes rely on system calls to perform operations beyond their own capabilities.*
## Command to see running processes
```
> ps -ef
```

#### macOS
![[Pasted image 20241124133724.png]]
UID -> owner

#### Linux
![[Pasted image 20241124134236.png]]

![[Pasted image 20241124134322.png]]
![[Pasted image 20241124134614.png]]

ppid - parent process ID [[Fork]]
![[Pasted image 20241124134337.png]]

## [[Fork]]
- *a [[System Calls|system call]]*
- only way a process can be created.
## [[Wait]]

