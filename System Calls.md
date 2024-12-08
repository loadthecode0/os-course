- [[CPU Modes of Operation]]
- Programme in user mode should make system calls to access protected resources.
	- Ask OS "Can you do this for me?"
	- One layer of abstraction

## How a system call transitions bw user space and kernel space
- ![[Pasted image 20241124114240.png]]
- fd - file identifier, buffer (array of characters in memory) - where to read to, nbytes- how much to read
#### User space operations:
- Push nbytes, buffer, fd -> onto the stack
- Call read() function rom the *library procedure*
	- wrapper provided in user space that interacts w the OS.
- Increment SP (stack pointer)
- **Trap to the kernel:** A special instruction (often called a **trap** or **software interrupt**) is executed to *transition control from user space to kernel space*. This ensures the OS gains control to perform privileged operations. -> ensures *security*

#### Kernel Space operations
- Dispatch: The kernel identifies the specific system call requested (ie read).
- **System Call Handler:** The kernel executes the system call handler for `read`, which:
    - Validates the file descriptor (`fd`).
    - Checks permissions.
    - Reads the requested number of bytes (`nbytes`) from the file or I/O device.
    - Copies the data to the memory buffer (`buffer`).
- Control returns to user space

#### Back to User Space
- Sys call completed, read() function in the library returns control to the user program.
- Increment SP: the stack pointer is adjusted to clean up the stack after the function call.

#### Error code / Status codes
- 0 if everything okay
- another for specific types of errors


## [[POSIX System Calls]]

## [[Processes]]
