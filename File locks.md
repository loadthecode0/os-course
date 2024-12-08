## File locks
- The OS can ensure that *only one process can open a file*
```c
while(1)
{
	lockf(LOCK);
	critical_region();
	lockf(UNLOCK);
}
```

## Example
![[Pasted image 20241207235213.png]]
![[Pasted image 20241207235234.png]]
output
![[Pasted image 20241207235339.png]]
no race conditions

