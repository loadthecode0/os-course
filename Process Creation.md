- Unix -> only thru [[Fork]]
- *All processes originate from the init process*

## New process initiation
- fork - new process
- exec - replace old code with another executable

## Memory sharing bw parent and child
![[Pasted image 20241205162502.png]]
- exact copies but different memories (address space)
- *each process has its own memory*
- no sharing of writable memory
- **Copy-on-write** -> create a copy of the file to be written to (optimization)
	- allows **multiple processes to share the same memory until one of them modifies it**, at which point a copy of the memory is created for the modifying process. 
	- minimizes unnecessary memory duplication and improves performance.