## x86 and x64
- x86 is the 32 bit implementation of the Intel architecture and x86-64 is the 64 bit version
- there are two modes of operation:
	- **Real** when the machine is first powered on and only supports 16-bit instruction set 
	- **Protected** supports virtual memory, paging and other features. This is the mode that most modern operating systems operate in 

#### Privelage Seperation
- done through an abstraction called the **ring level**, it supports:
	- Ring 3 is lowest privelage level and can only read/modify a subset of system settings
		- usually considered user mode by most operating system
	- Ring 0 is the highest level of privelage and is often refered to as the kernel 
- the ring level is encoded in the *cs* register and is often refered to as the current privelage level(CPL) in the documentation 

#### Register Set
- x86 protected mode architecture features eight 32-bit general purpose registers(GPR)
	- **EAX** -- can split into 16 bit *AX* or 8 bit *AH* and *AL*
	- **ESI** -- used for source in string/memory ops | can be split into 16 bit *SI*
	- **EDI** -- destination in string/memory ops | can be split into 16 bit *DI*
	- **EBP** -- base frame pointer(original location of ESP) -- can be split into 16 bit *BP*
	- **ESP** -- stack pointer -- can be split into 16 bit *SP*
	- **EIP** -- instruction pointer
	- **EFLAGS** -- contains execution flags
		- *ZF*
	- **MSR** -- model specific registers may exist 

#### Data Types
- **Bytes** -- 8bits
- **Word** -- 16 bits
- **Double Word** -- 32 bits
- **Quad Word** -- 64 bits, created by combining two registers(usually EDX:EAX)

#### Instruction Set 
- assembly is amazing in that it allows for a high level of flexibility in terms of data movement, there are 5 general methods:
	- Immediate to register
	- register to register
	- immediate to memory 
	- register to memory and vice versa
	- Memory to memory
		- specific to x86
- In classical architectures you have to read from memory, change the value and write it back to memory, compared to x86 where you can modify memory in place. 
- we will be using intel notation but be aware the AT&T notation does exist

#### Data Movement
- the most common instruction is MOV 
- simpliest usage is to move a register or immediate to register
```x86
mov esi, 0F003Fh ; SET ESI = 0xF003
mov esi, ecx.    ; SET ESI = ECX
```
- another usage is moving to/from memory, x86 uses [] to indicate memory
	- size directive ptr is utilized to indicate the size of the data
- in the following examples we use registers as storing memory addresses which is frequently done for complex data types 
```x86
mov dword ptr [eax], 1 ; [eax] is the same as *eax in C++
; Move double word sized 1 into memory whose location is stored at eax\
mov [esi+34h], eax
; set the memory at address (esi+34) to eax
```
