## Section 1 - Short answer
1) ![[Pasted image 20241128090809.png]]
	- [x] watch lecture
	- heap memory
	- shared variables
	- global variables
1) ![[Pasted image 20241128090900.png]]
	- flexibility, modularity, stability
	- easier to maintain and update
2) ![[Pasted image 20241128091705.png]]
	![[Pasted image 20241128091228.png]]
	- all code is copied, but separate address spaces
	- so counter pointer is also different for both child and parent processes HOWEVER the value held in both is same 
	- so prints 2 for child inside if statement and 2 outside as well
	- prints 1 for parent after child is exited
	- ans:
```
2
2
1
```
1) ![[Pasted image 20241128091214.png]]
	- ![[Pasted image 20241128091730.png]]
	- assuming that all invocations are successful
	- so pid = 0
	- due to shorter sleep period, the child process terminates earlier
	- so the process is already dead when the parent process sends the KILL signal, hence there would be an error : "Failed_to_send_SIGKILL"
	- **This was wrong**
	- the child executes the statements in a while loop.
	- the parent waits for two sleep cycles and then kills the child process.
	- output:
```
Child:45650
Hello
Child:45650
Hello
SIGKILL_signal_sent_to_child_process
```

1) ![[Pasted image 20241128092612.png]]
	- ![[Pasted image 20241128092626.png]]
	- again two separate copies of address space for parent and child processes
	- [x] waitpid() ??
	- the child process terminates due to exit(0) before printing
	- only the parent process prints
	- output = '3'
	- The outcome will be: 3
	- Child will reach exit before it reaches a print statement. Each process has its own version of the global variable counter, so it will print the variable of the parent, which is 3.
1) ![[Pasted image 20241128093123.png]]
	- ![[Pasted image 20241128093136.png]]
	- [!] didn't watch lecture
	- guess - any one which is mapped to physical mem and contains a value? 
2) ![[Pasted image 20241128093436.png]]
	![[Pasted image 20241128093451.png]]
	- 4 times
	- **Wrong**
	- 7 times
	- ![[Pasted image 20241208004759.png]]
1) ![[Pasted image 20241128093855.png]]
	![[Pasted image 20241128093909.png]]
	- count function print dereferenced value after casting a to an int pointer
	- all threads access the same address space, so &i is same for all.
	- it will print the values of i from 0 to 9, BUT not in order because the multithreading is pseudo-parallel. It can be any random order depending on runtime hardware properties.
	- **Wrong**
	- Random output:
	- Each thread starts executing and tries to print the value of i before the loop has finished. The value of i keeps changing during the loop, so threads may read different values based on when they start executing. By the time the first thread executes, i might have already incremented, and the other threads may print values that reflect the incremented i, leading to an unexpected order of output.
1) ![[Pasted image 20241128094443.png]]
	- [!] didn't watch lecture
	- guesses - communication problem in distributed memory, waiting times, memory transfer bottlenecks
2) ![[Pasted image 20241128094612.png]]
	- high priority, because they are significant contributors to user interaction, and it would not be a nice thing to keep users waiting for computers to take inputs and outputs. Bg processes can be low priority.
3) ![[Pasted image 20241128094753.png]]
	- FIFO is just a queue
	- unlike an LRU strategy, FIFO doesn't reupdate the recently used pages. So it doesn't account for temporal and spatial locality. If the page was the first to enter, it may not necessarily mean that it is the least recently used and can be pushed out of the queue.

## Long Questions
1) ![[Pasted image 20241128095053.png]]
- [!] watch the freaking lecture

2) ![[Pasted image 20241128095201.png]]
		![[Pasted image 20241128095347.png]]
		
	
3) ![[Pasted image 20241128095211.png]]
- [!] lecture. watch. pls.