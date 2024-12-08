- unidirectional data channel (special file)
- used for interprocess communication
- connects output of one process to input of another
- [[System Calls]]:
	- `int pipe(int pipefd[2]); //creates a pipe`
	- `int dup2(int oldfd, int newfd); //creates a copy of a file descriptor, using the new file descriptor`

## Class example
![[Pasted image 20241205150934.png]]
- pipe for communication bw parent and child processes
- pipe(link)-> *creates pipe AND assigns the file descriptors*
- child process writes msg to the pipe,
- parent reads msg from the pipe and prints it
- link[0] -> read end, link[1] -> write end
- close(link[0]) -> closes the read end of the pipe (not needed)
- Output:
![[Pasted image 20241205151548.png]]

## Class example 2
![[Pasted image 20241205151730.png]]
- output is just output of ls