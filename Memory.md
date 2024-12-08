- We want to balance fast, large, cheap -> can get only 2 out of 3
- **layered memory**
	- ![[Pasted image 20241123180342.png]]
- RAM = main memory
	- not permanent
- Magnetic disk
	- permanent
- Caches follow principle of locality
	- *A programme accesses a relatively small portion of address space at any instant of time*
	- Temporal vs spatial locality
	- implications for programming
		- double array example
		- code must exhibit locality
		- make sure any data reuse is shortly after prior use
		- cluster reused data together
		- cluster together data accessed shortly after each other
![[Pasted image 20241123181025.png]]
L1 < L2 < L3 (cache access time, size)
First image has shared L2 cache
tradeoffs between these
- coordination for shared cache but efficient sharing

## CPU configs
```
> lscpu
> getconf -1 | grep -i cache
```

## [[Memory Management]]