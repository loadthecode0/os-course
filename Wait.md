
![[Pasted image 20241124145111.png]]
- parent has to read the returned exit code from the child
	- *exit code is a form of communication*
	- but if parent terminates earlier, there is no process to read the exit code form the child -> not cleaned up from process table -> **zombie process**
	- the child is adopted by the OS (parent pid = 1 then)

The `waitpid()` function in C is used by a process to **wait for state changes in one of its child processes**. It **allows the parent process to retrieve the exit status or other information about the child process**.

---

### **Prototype**

```c
#include <sys/types.h>
#include <sys/wait.h>

pid_t waitpid(pid_t pid, int *status, int options);
```

---

### **Parameters**

1. **`pid`**:
    - Specifies which child process to wait for. It can take specific values:
        - **`pid > 0`**: Waits for the child process with the specified PID.
        - **`pid == 0`**: Waits for any child process in the same process group as the calling process.
        - **`pid < -1`**: Waits for any child process in the process group with the absolute value of `pid`.
        - **`pid == -1`**: Waits for any child process (default behavior, equivalent to `wait()`).
2. **`status`**:
    - A pointer to an integer where the child's exit status or other information is stored. Use macros like `WIFEXITED`, `WIFSIGNALED`, etc., to interpret this status.
3. **`options`**:
    - Modifies the behavior of `waitpid()`. Common values:
        - **`WNOHANG`**: Returns immediately if no child has exited (non-blocking).
        - **`WUNTRACED`**: Returns if a child has stopped (e.g., by `SIGSTOP`).

---

### **Return Value**

- **PID of the child**: On success, `waitpid()` returns the PID of the child process whose state has changed.
- **0**: If `WNOHANG` is specified and no child process has exited.
- **-1**: On error, with `errno` set to indicate the error (e.g., if no child processes exist).

---

### **Macros for Interpreting the Status**

Use the following macros (defined in `<sys/wait.h>`) to interpret the `status` value:

1. **`WIFEXITED(status)`**:
    - Returns true if the child process terminated normally (e.g., via `exit()`).
    - Use `WEXITSTATUS(status)` to retrieve the exit code.
2. **`WIFSIGNALED(status)`**:
    - Returns true if the child process was terminated by a signal.
    - Use `WTERMSIG(status)` to retrieve the signal number.
3. **`WIFSTOPPED(status)`**:
    - Returns true if the child process is currently stopped (e.g., via `SIGSTOP`).
    - Use `WSTOPSIG(status)` to retrieve the signal number.
4. **`WIFCONTINUED(status)`**:
    - Returns true if the child process has resumed execution (e.g., after `SIGCONT`).

---

### **Example: Basic Usage**

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("Fork failed");
        return 1;
    } else if (pid == 0) {
        // Child process
        printf("Child process: PID = %d\n", getpid());
        sleep(2);
        exit(42); // Exit with a specific status
    } else {
        // Parent process
        int status;
        pid_t child_pid = waitpid(pid, &status, 0); // Wait for the specific child process

        if (child_pid == -1) {
            perror("waitpid failed");
            return 1;
        }

        if (WIFEXITED(status)) {
            printf("Child %d exited with status %d\n", child_pid, WEXITSTATUS(status));
        } else if (WIFSIGNALED(status)) {
            printf("Child %d terminated by signal %d\n", child_pid, WTERMSIG(status));
        }
    }

    return 0;
}
```

---

### **Output**

```
Child process: PID = 12345
Child 12345 exited with status 42
```

---

### **Common Use Cases**

1. **Waiting for a Specific Child**:
    - `waitpid()` is useful when the parent has multiple children and needs to wait for a particular one.
    - *blocking of parent process until child process finishes.*
1. **Non-blocking Wait**:
    - Using the `WNOHANG` option allows the parent to periodically check on the child without blocking execution.
2. **Handling Child Termination**:
    - Retrieve the exit status of child processes to manage their outcomes.

---

### **Key Differences Between `wait()` and `waitpid()`**

|**Feature**|**`wait()`**|**`waitpid()`**|
|---|---|---|
|Wait for specific child?|No|Yes|
|Non-blocking option?|No|Yes (`WNOHANG`)|
|Wait for stopped child?|No|Yes (`WUNTRACED`)|

---

`waitpid()` is a more flexible and powerful alternative to `wait()` and is essential for managing processes in complex multitasking applications.


## Example from class
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
  

int main(void)
{
	
	int counter = 0;
	counter = 100;
	printf("[%d] I am the parent process and I fork.\n", getpid());
	pid_t pid = fork(); // fork a child process
	if (pid == -1)
	{
		printf("fork fail\n");
		exit(1);
	}

	if (pid == 0) 
	{
		// child process
		// code execution
		printf("[%d] I am the child process and I execute some code.\n", getpid());
		char c = getchar(); // emulating a slow execution...
		int return_code = 58;
		printf("[%d] I am the child process and I return: %d\n", getpid(), return_code);
		return return_code;
	}
	
	else 
	{
	// parent process
		printf("[%d] I am the parent and I will wait for the child %d to terminate.\n", getpid(), pid);
		int child_status;
		waitpid(pid, &child_status, 0); // waiting for the child to return
		printf("[%d] The child process returned: %d\n", getpid(), WEXITSTATUS(child_status) );
	}
	return 0;
}
```

- waitpid(pid, &child_status, 0) -> 0 indicates default blocking behaviour (until the specified child process terminates or changes state, i.e, exits or is stopped by a signal).
#### Output:
![[Pasted image 20241204163454.png]]
