- Clone of a process
- parent and child 
- **exact copy**
	- different address space but exact same contents
- **only way a process can be created**
- Both parent and child processes execute the remaining code **from the same point** but with their own memory and execution contexts.Both parent and child processes execute the remaining code **from the same point** but with their own memory and execution contexts.
- ![[Pasted image 20241124134726.png]]
- [!] see the parent child relationships in this table!
- All processes are children of the init process
- `> pstree`
- For the parent fork() returns the child's PID (positive integer)
- For the child fork() returns 0 (inside the child process)
- -1 is error (in case no child process is created)
- The return 0 from child is returned to the parent
- *Both processes execute the code following the `fork()` call, but they can distinguish themselves based on the return value of `fork()`.*
- *There is no deterministic order of execution of parent and child processes.*
	- Use [[Wait]] to enforce specific execution order.
## Fork Code Demo

#### 1

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main(void)

{
	int counter = 100;
	printf("[%d] I am the parent process and I fork.\n", getpid());
	
	pid_t pid = fork(); // fork a child process
	if (pid == -1) { // error checking
		printf("fork fail\n");
		exit(1); // exit with exit code 1
	}
	
	printf("[%d] Both parent and child will execute this.\n", getpid()); -> since code is copied exactly.
	
	if (pid == 0) {
		// child process
		printf("[%d] I am the child process and my parent is: %d\n", getpid(), getppid());
		sleep(1);
		int i;
		for (i=0;i<5;i++) {
			printf("[%d] child process: counter=%d\n", getpid(), ++counter);
		}
	}

	else {
		// parent process
		printf("[%d] I am the parent process and my parent is: %d\n", getpid(), getppid());
		sleep(1);
		int i;
		for (i=0;i<5;i++) {
			printf("[%d] parent process: counter=%d\n", getpid(), ++counter);
		}
	
	}

  

//char c = getchar();
return 0;

}
```

- the if statement separates the child and parent processes
- Output:
	![[Pasted image 20241124135927.png]]

#### 2 - global variable pointing to heap
![[Pasted image 20241124140009.png]]
 ![[Pasted image 20241124140307.png]]
- each works in its own copy of heap memory


## Shared Memory
- After fork, parent and child process have different address spaces
- can't exchange data via the global variables or heap
- it is possible to ask OS for some shared memory.
- [[System Calls]] - mmap instead of malloc
	- `A = mmap(NULL, sizeof(int), PROT_READ | PROT_WRITE, MAP_SHARED | MAP_ANONYMOUS, -1, 0);`
- ![[Pasted image 20241124144601.png]]
- We don't know if child or parent will execute first.
- may lead to race conditions
- ![[Pasted image 20241124144641.png]]

## Orphan Process
![[Pasted image 20241124144823.png]]
![[Pasted image 20241124144910.png]]
![[Pasted image 20241124144916.png]]
1 -> init process
## [[Wait]]

## [[Signals]]

## [[Exec]]

## [[Stat]]
