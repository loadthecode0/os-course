- similar philosophy to caches
- [!] go through replacement ideas again
- if removed page is modified, then hard disk copy must be updated
- goal -> minimise number of page faults.
- Ideally
	- want to remove the one that will be referenced last
	- theoretically optimal
	- not very practical
		- we can't know with certainty

### Not Recently Used (NRU)
![[Pasted image 20241208121956.png]]
- **Limitation**
	- No temporal boundaries -> A pages referenced 21ms ago is treated equally to one referenced 1ms ago.

### FIFO (First In First Out)
![[Pasted image 20241208122218.png]]
- **Limitation**
	- Just cuz something is loaded first, doesn't mean that is will be less useful
	- age is not a good indicator of usefulness

### Second Chance
- combines the above two approaches
- remove the oldest page that has not been referenced recently
- ![[Pasted image 20241208122358.png]]
- **Limitation:** extra overhead of moving pages around

### Clock
![[Pasted image 20241208122454.png]] 

### Least Recently Used (LRU)
- remove the page that has been unused for the longest time
- close approximation of the optimal strategy
- ![[Pasted image 20241208123140.png]]
- not a practical idea
- need timing statistics of how long everything has been referenced.

### Not Frequently Used (NFU)
![[Pasted image 20241208123235.png]]


## Ageing
![[Pasted image 20241208123715.png]]
- [!] re-understand
- using shift and insert ops  -> efficient in hardware

## Working Set
![[Pasted image 20241208123923.png]]
- *Remove page not in working set*
- expensive somewhat

## WS Clock
![[Pasted image 20241208124341.png]]



## Summary
![[Pasted image 20241208124555.png]]
- can use optimal as a benchmark
- deciding what to keep in memory vs storage