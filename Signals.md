- another form of communication bw processes (apart from exit codes) OR bw processes and OS.
```
> kill -l
```
Output:
```
HUP INT QUIT ILL TRAP ABRT EMT FPE KILL BUS SEGV SYS PIPE ALRM TERM URG STOP TSTP CONT CHLD TTIN TTOU IO XCPU XFSZ VTALRM PROF WINCH INFO USR1 USR2
```
- These are different types of signals
- *Signals are software-based interrupts:*
	- interrupt the normal execution to run a **handler function**
		- -> need to register a signal handler
	- A default signal handler is executed unless the process has registered a custom signal handler.
	- Some signals can't be caught or ignored.
- *System calls:*
	- ![[Pasted image 20241127112505.png]]
- [n] ideas are still a bit fuzzy, give more time.

## **Signal handlers**
A **signal handler** is a function defined by the user that is executed when a specific **signal** is delivered to a process. Signal handlers allow a process to perform custom actions in response to signals, instead of taking the default action (e.g., terminating the process).

## Termination
### Class example
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>

void handler(int sig) {
	if (sig == SIGINT) {
	printf("\nLooks like you hit Ctrl-C. I ignore you!\n");
	}
	
	else if (sig == SIGTERM) {
	printf("Looks like you sent me a termination signal. I still ignore you!\n");
	}
}

int main(void) {

	signal(SIGINT, handler); // setting up the same handler for two signals
	signal(SIGTERM, handler);
	
	while(1){
	printf("[%d] Loop\n", getpid());
	sleep(1);
	}
	
	return 0;
}
```

#### Output
![[Pasted image 20241204164342.png]]
![[Pasted image 20241204164510.png]]
- maybe for graceful termination e.g cleaning
- use `SIGKILL` -> not overwriteable!!! `kill -9 11698`

## Alarm
### Class example
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h> 

int flag = 1;
void alarm_handler(int sig) {

if (sig == SIGALRM) {
	flag = 0;
	}
}

int main(void) {
	int counter = 0;
	signal(SIGALRM, alarm_handler); // setting up a handler for the alarm signal
	printf("I am setting an alarm signal in 5 seconds\n");
	alarm(5);
	while(flag == 1) {
		printf("Loop\n");
		sleep(1);
	}
	printf("Done.\n");
	return 0;
}
```
#### Output
![[Pasted image 20241204165546.png]]