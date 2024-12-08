- Communication bw threads
	- Inter-process - threads of the different processes
	- intra-process - threads of same process
![[Pasted image 20241207120439.png]]

## Ways to communicate
- **Shared memory**
	- Global variables, heap memory
		- (threads only!)
	- shared memory in the kernel
	- files
- **Messages and data streams**
	- signals
	- pipes
	- sockets (UDP, TCP, UNIX)
- [[Files#Interprocess Communication through files|Communicating through files]]

### Example 1 - race conditions with fork
![[Pasted image 20241207210431.png]]
![[Pasted image 20241207210440.png]]
output
![[Pasted image 20241207210647.png]]
- Why this? 
	- We don't know about the scheduling
	- first child process can be interrupted by the second child process before writing is done.
	- [[Race conditions]]
### Example 2 - Murphy's Law
- anything that can go wrong will go wrong - something will definitely go wrong if done many times.
![[Pasted image 20241207211310.png]]

### Example 3 - Race conditions with Threads
![[Pasted image 20241207211806.png]]
output
- different outcome every time
- ![[Pasted image 20241207212211.png]]
- again - scheduler interrupting and cpu switching - [[Race conditions]]

## [[Race conditions]]

## [[Race conditions#Avoiding Race Conditions|Avoiding Race Conditions]]

### [[Strict Alternation]]

### [[Hardware based solutions to race conditions]]

## [[Deadlocks]]

## [[Inefficient busy waiting]]
## Semaphores vs Mutexes
![[Pasted image 20241208001834.png]]

## Message Passing
![[Pasted image 20241208001919.png]]
### Solving the producer consumer problem
![[Pasted image 20241208002150.png]]