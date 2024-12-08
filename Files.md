- **data container** probably on disk
- **Directories** group files together
- Organised in **trees**

## File descriptor
- assigned to each file
- a number
- **handle** to access files

## File Permissions
- bitmap of 9 digits
- `> ls -al`
- ![[Pasted image 20241204171339.png]]
	- specifies what permissions they have - read/write/execute
- [[System Calls]]:
	- `int chmod (const char *path, mode_t mode) //permission change`

## Everything in UNIX is a file (descriptor)!
![[Pasted image 20241205140722.png]]
- special files
- terminal redirection tools
- standard file descriptors

## Class example
### 1 - STDOUT, STDERR
```c
#include <stdio.h> 
#include <stdlib.h>

#include <unistd.h> 
//Provides access to the POSIX operating system API, including `getpid()` and file descriptor macros like `STDOUT_FILENO`.

#include <fcntl.h>
// Contains file control options, like `O_WRONLY` and `O_CREAT`, used for file operations.

int main(void) {

	dprintf(STDOUT_FILENO, "[%d] I print this in STDOUT (fd = %d) \n", getpid(), STDOUT_FILENO);
	dprintf(STDERR_FILENO, "[%d] I print this in STDERR (fd = %d) \n", getpid(), STDERR_FILENO);
	
	int fd = open("./temp.txt", O_WRONLY | O_CREAT, 0644);
	
	dprintf(fd, "[%d] I print this in file (fd = %d) \n", getpid(), fd);
	close(fd);
	
	return 0;
}
```

- dprintf is like printf but you can pass a file descriptor as an argument
### Output
![[Pasted image 20241205143217.png]]
![[Pasted image 20241205143226.png]]
- file descriptor for STDOUT is 1 and that for STDERR is 2.
- `O_WRONLY`: Open the file in *write-only* mode.
- `O_CREAT`: Create the file if it does not exist.
- `0644`: File permissions: Read/write for the owner, read-only for group and others.
- ![[Pasted image 20241205143827.png]] 
	- redirected error to 'log' file
- [!] ![[Pasted image 20241205144055.png]]
	- by default, the redirection considers the standard output
	- 1) the default is stdout, redirected to foo
	- 2) same as 3
	- 3) - `2>1` tries to redirect **stderr** to a file named `1` (not to stdout!).
		- `>` redirects **stdout** to `foo`.
		- Since `1` is treated as a regular file, only **stderr** is written to `1`, while **stdout** is written to `foo`.
		- **Terminal**: Nothing (stderr and stdout are both redirected elsewhere).
		- **`1`**: (if you checked the file `1`) would contain:`[15938] I print this in STDERR (fd = 2)`
	- the last case redirects the err to out and all of out to foo
### 2 - STDIN
- ![[Pasted image 20241205145715.png]]
- last -> read from foo and redirect output to bar.

### Pipe (|)
- redirect the **standard output (stdout)** of one command into the **standard input (stdin)** of another command. 
- allows multiple commands to be chained together, passing data from one command to another.
- The output of the command on the **left side** of the pipe (`|`) is passed as the input to the command on the **right side**.
    - The shell creates a **pipe buffer** in memory, which temporarily holds the data between the two commands.
- **Chaining Commands**:
    - Multiple commands can be chained together using multiple pipes.
    - Example: `command1 | command2 | command3`.
- **Unidirectional**:
    - Pipes only pass data from **left to right**. If bidirectional communication is needed, other mechanisms like sockets or FIFOs are required.

#### **Basic Example**

```bash
ls | wc -l
```

- **What It Does**:
    - `ls`: Lists the files in the current directory.
    - `wc -l`: Counts the number of lines in the input.
- **Result**:
    - Prints the number of files in the current directory.
#### **Combining with Redirection**:
    
- Pipes can be combined with file redirection (`>`, `>>`, `<`, etc.).
	```bash
	ls | grep "txt" > output.txt
	```
	- Writes the filtered output of `grep` to `output.txt`.
#### **Error Handling**:
    
- By default, pipes only redirect **stdout**. To include **stderr**, you can redirect it explicitly:
	```bash
	command1 2>&1 | command2
	```
	
#### **Filter Example**

```bash
cat file.txt | grep "error"
```

- **What It Does**:
    - `cat file.txt`: Outputs the contents of `file.txt`.
    - `grep "error"`: Filters lines containing the word "error".
- **Result**:
    - Prints all lines in `file.txt` that contain the word "error".

#### **Multiple Pipes**

```bash
ps aux | grep apache | awk '{print $2}'
```
- **What It Does**:
    - `ps aux`: Lists all running processes.
    - `grep apache`: Filters processes related to "apache".
    - `awk '{print $2}'`: Extracts and prints the second column (process IDs).
- **Result**:
    - Displays the process IDs of all running Apache processes.

---

#### **Behind the Scenes**
- The shell creates two processes:
    1. The process for the command on the left of the pipe.
    2. The process for the command on the right of the pipe.
- A pipe buffer is created in memory to transfer data between these processes.
- The first command writes to the pipe buffer, and the second command reads from it.
#### **Sort and Filter**

```bash
ls | sort | uniq
```

- Lists all files, sorts them, and removes duplicate entries.

#### **Count Specific Words**

```bash
cat file.txt | grep -o "word" | wc -l
```

- Counts the occurrences of the word "word" in `file.txt`.

#### **Search Logs for Errors**

```bash
tail -f /var/log/syslog | grep "error"
```

- Continuously monitors the system log for lines containing the word "error".

---


## File descriptors are local to a process
Each process maintains its own table of file descriptors, which is used to track open files and other resources like sockets or pipes.


## Interprocess Communication through files

