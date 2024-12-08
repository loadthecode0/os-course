- Threads can be implemented either at user or kernel level

## Scheduling user level threads
- these threads are not present to the kernel
- The kernel views the entire process (containing these threads) as a single entity.
![[Pasted image 20241206134712.png]]
- the kernel doesn't know about the threads in the process, it schedules the process containing them.
- thread switching only happens at specific points (e.g., when a thread yields or completes), not due to preemption by the OS.
## Scheduling kernel-level threads
![[Pasted image 20241206134726.png]]
- The operating system's **kernel scheduler** is responsible for scheduling individual threads instead of treating the process as a whole.
- The kernel has full knowledge of all threads.
- The kernel can preempt threads, ensuring that no single thread monopolizes the CPU.
- The kernel can schedule threads on multiple cores, enabling true parallelism for multi-threaded applications.
- **Blocking Operations**:
    - If a thread blocks (e.g., waiting for I/O), the kernel can schedule another thread in the same process, improving efficiency.