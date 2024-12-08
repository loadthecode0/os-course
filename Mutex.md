## Mutex
![[Pasted image 20241207233550.png]]
- yields the cpu to another thread when the mutex is busy
### Avoiding race conditions with mutexes
pseudocode
```c
while(1)
{
	mutex_lock();
	critical_region();
	mutex_unlock();
}
```

### Mutexes in pthread
- mutexes can **protect** shared variables (global, heap) among threads within a process.
- mutexes can protect shared memory and files among threads in different processes -
	- *the mutex must be allocated in the shared memory*
- ![[Pasted image 20241207234208.png]]
- or block/fail is what happens if lock acquire fails.
- ![[Pasted image 20241207234340.png]]
- ![[Pasted image 20241207234348.png]]
- output -> no race condition

