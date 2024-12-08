## Controller
- I/O devices generally have a **controller**.
- Controller
	- mini chip whioch physically controls the device on behalf of the computer
	- controllers 
		- have processors (non programmable)
		- have registers
		- may have memory
		- accepts commands from OS
	
## Device driver
- A piece of **software** in OS that talks to the controller
- How do we put a driver in the kernel?
	- old -> relinking kernel
	- then -> booting
	- now -> on the fly (plug and play)

## Accessing the memory/registers of I/O devices
### Abstraction, i.e, memory-mapped I/O: 
- map to system's address space
- R/W as any other memory address. -> triggers an action on the device.
### Communication
3 types of communication:
#####  *Busy waiting, i.e, polling*: 
send command, check if done in loop -> wastes CPU cycles.
##### *Interrupt based*: 
send command and sleep, controller generates an interrupt to signal completion of I/O device task. -> efficient
- *Interrupt controller:* a hardware component that manages multiple interrupt requests from different devices and sends them to the CPU in an organised manner (based on priority).
		- can be a wire connection
		- ![[Pasted image 20241123182931.png]]
		- Left image
			- here disk controller is the I/O device. magnetic disk takes time to read.
			- Step 1 is task initiation (command to controller to start task)
			- Step 2 - disk controller notifies completion - signals the interrupt controller to inform CPU that op is finished.
			- step 3- the interrupt controller sends *IRQ (interrupt request)* to CPU -> forces the CPU to pause its current task and handle the interrupt.
			- Step 4 - the CPu interacts w the interrupt controller to identify the source of the interrupt and dispatches the appropriate interrupt handler to process the event.
		- Right image
			1) Interrupt Signal Received: The CPU receives the interrupt signal while it is executing a current instruction.
			2) Save CPU State: Before handling the interrupt, the CPU saves the current execution state (e.g., program counter and registers). This allows it to return to the same point after the interrupt is serviced.
			3) Dispatch to Interrupt Handler: The CPU executes *the interrupt handler, a specific piece of code designed to deal with the interrupt* (e.g., reading data from the disk or updating I/O buffers).
			4) Return to Main Program: Once the interrupt handler finishes, the CPU restores its saved state and resumes execution of the interrupted program.
##### *DMA (Direct memory access)*: 
a special chip that can move data between controller and main memory without the involvement of the main CPU. -> efficient, CPU is not burdened with data transfer.