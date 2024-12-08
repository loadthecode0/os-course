- below are codes for processes A and B respectively
- processes take turns 
	- only the process with the matching turn value can proceed to the CR
	- when A exits the CR, it gives the turn to B and vice versa
![[Pasted image 20241207214737.png]]

- *free from the race conditions*
- **Problem**
	- A process can't enter the critical region twice in a row
		- so a slow process would slow down a fast process.
	- **Inefficiency Due to Busy Waiting**:
		- A process that cannot enter the critical region spends its time in the `while` loop, **wasting CPU cycles**.