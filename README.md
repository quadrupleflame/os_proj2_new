#os-team20

## How to Build
$ ./build

to build the test code, type
$ arm-linux-gnueabi-gcc -I /include test.c -o test
$ sdb root on
$ sdb push test /root/test

in debug console
$ direct_set_debug.sh --sdb-set
$ /root/test

##High-Level Design & implementation
1.
2.
3.

```c
st

##Lessons Learned
* custom scheduler를 구현하는 방법을 알게되었다.
* test파일을 작성하면서 prime factorization naive tiral division method에 대해 알게되었다.

## How To Register System Call
### 1. Increment the number of System calls
in file: "arch/arm/include/asm/unistd.h"
``` c
#define __NR_syscalls  (N)
```
to
```c
#define __NR_syscalls  (N+4)
```
Total number of system calls must be a multiplication of 4.

### 2. assign system call number
in file: "arch/arm/include/uapi/asm/unistd.h"
add
```c
#define __NR_myfunc      (__NR_SYSCALL_BASE+ #) 
```

### 3. make asmlinkage function
in file: "include/linux/syscalls.h"
```c
asmlinkage int my_func()  // if no parameter then write 'void' 
```

### 4. add to system call table
in file: "arch/arm/kernel/calls.S"
```
call(sys_myfunc)
```

### 5. Revise Makefile
in file: "kernel/Makefile"
```
obj -y = ...  ptree.o
```

### etc.
in file: "kernel/myfunc.c"  
the name of function must be sys_myfunc()
