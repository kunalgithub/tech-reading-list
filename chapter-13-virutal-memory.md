## Learning about pmap 

### Homework 

```
7. Now run pmap on some of these processes, using various flags (like -X) to reveal many details about the process. What do you see?
How many different entities make up a modern address space, as opposed to our simple conception of code/stack/heap?
```

I ran the following command. 

`while true ; do sleep .1 ;pmap -X $(pgrep -f memory-user) >> memory-user-monitoring.out ; done`

- Heap is allocated 132 KB and does not grow as the program runs
- Stack is allocated 132 KB and does not grow as the program runs
- The code is allocated 20KB, but it's not clear.

- The `code` allocation is shown below , it shows 4 Mappings for `memory-user`

  ```
           Address Perm   Offset Device    Inode   Size   Rss   Pss Pss_Dirty Referenced Anonymous KSM LazyFree ShmemPmdMapped FilePmdMapped Shared_Hugetlb Private_Hugetlb Swap SwapPss Locked THPeligible ProtectionKey Mapping
    569e6899d000 r--p 00000000  fc:01 12453906      4     4     4         0          4         0   0        0              0             0              0               0    0       0      0           0             0 memory-user
    569e6899e000 r-xp 00001000  fc:01 12453906      4     4     4         0          4         0   0        0              0             0              0               0    0       0      0           0             0 memory-user
    569e6899f000 r--p 00002000  fc:01 12453906      4     4     4         0          4         0   0        0              0             0              0               0    0       0      0           0             0 memory-user
    569e689a0000 r--p 00002000  fc:01 12453906      4     4     4         4          4         4   0        0              0             0              0               0    0       0      0           0             0 memory-user
    569e689a1000 rw-p 00003000  fc:01 12453906      4     4     4         4          4         4   0        0              0             0              0               0    0       0      0           0             0 memory-user

   ```
8. Finally, let’s run pmap on your memory-user program, with different amounts of used memory. What do you see here? Does the output from pmap match your expectations?
```

