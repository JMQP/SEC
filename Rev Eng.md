# X86_64 Assembly

There are 16 general purpose 64-Bit registers


%rax

the first return register

%rbp

the base pointer that keeps track of the base of the stack

%rsp

the stack pointer that points to the top of the stack



You will see arguments passed to functions as something like:

[%ebp-0x8]


# X86_64 Assembly - Common Terms
HEAP

Memory that can be allocated and deallocated

STACK

A contiguous section of memory used for passing arguments

GENERAL REGISTER

A multipurpose register that can be used by either programmer or user to store data or a memory location address

CONTROL REGISTER

A processor register that changes or controls the behavior of a CPU

FLAGS REGISTER

Contains the current state of the processor


# X86_64 Assembly - Memory Offset

There is one instruction pointer register that points to the memory offset of the next instruction in the code segment:


64-Bit	

RIP

Lower 32 bits	

EIP

Lower 16 bits	Descrition

IP

Instruction Pointer; holds address for next instruction to be executed

# X86_64 Assembly - Common Instruction Pointers
MOV

move source to destination

PUSH

push source onto stack

POP

Pop top of stack to destination

INC

Increment source by 1

DEC

Decrement source by 1

ADD

Add source to destination

SUB

Subtract source from destination

CMP

Compare 2 values by subtracting them and setting the %RFLAGS register. ZeroFlag set means they are the same.

JMP

Jump to specified location

JLE

Jump if less than or equal

JE

Jump if equal

# Reverse Engineering Workflow (Software)
Static

	Initial static analysis of a binary gives an analyst, or team of analysts, several clues as to what the
	binary is designed to do and how it really works

Behavioral

	Behavioral Analysis is the fastest way to gain insight into how a binary works.

Dynamic 

	Dynamic analysis is similar to behavioral, except the analyst is attaching the process to a debugger

Disassembly

	An analyst will eventually get to a point where they need to disassemble a binary to learn more
	about how it runs

Document Findings

	Analysts must document their findings after performing reverse engineering or software analysis.

![image](https://github.com/user-attachments/assets/88ce8329-744c-4b02-95b5-7f7f8edde4f1)

# DEMO 

***Action + Destination + Value)***

mov r15,#n <- *Moving #n into r15*

mov rax,m <- *Move m into rax*

push m,rax <- *Move value in rax to m*

push r15 <- *Pushes r15 to the (Top of) stack*

pop r8 <- *Pop r8 off the top of the stack*

inc r8 <- *increment value in r8 by 1*

dec r8 <- *decrement value of r8 by 1*

add r13,64 <- *add 64 to r13, store in r13*

sub r13,16 <- *subtract 16 from r13, store result in r13*

cmp r8, r9 <- *Compare value of r8 to r9 , the zero flag will be set.*

jmp MEM1 <- *jump to MEM1*

jle MEM1 <- *jump to MEM1 if zero flag set less than or equal*

je MEM1 <- *jump to MEM1 if zero flag set to equal*

# DEMO 2
```
main:
	mov rax, 16 -> move 16 into rax
 	push rax 	-> push value rax (16) onto stack. RSP is pushed by 8 bytes (64 bits)
  	jmp mem2 	-> jmp to mem2 (Skips over mem1)

mem1:
	move rax, 0 -> move 0 to rax
 	ret			-> return out of code


mem2:
	pop r8 		-> pop value on stack (16) into r8. RSP falls by 8 bytes
	cmp rax, r8 -> compare value rax (16) to r8 (16) equal zero flag set
 	jmp mem1 	-> jump to mem1 if equal zero flag set
```

# Demo 3
```
main:
	mov rcx, 25 -> store the value 25 in rcx reg
 	mov rbx, 62	-> store value 62 in rbx reg
  	jmp mem1	-> jumps to mem1

mem1:
	sub rbx, 40 -> subtract 40 from rbx (22)
 	mov rsi, rbx-> copy rbx value to rsi (22)
  	cmp rcx, rsi-> compare the values in rcx and rsi sero flag less than
   	jmple mem2  -> jumps to mem2 location if value is less than or equal 

 mem2:
 	mov rax, 0  -> store 0 in rax
	ret			-> return out of code
```

# RDP DEMO
```
#include <windows.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int firstKey(key1)
{
    int key2 = atoi(key1);   //setting variable key2 setting to value of key1
	int p2 = 29;             //set variable p2 to 29
    if ((key2-123)==0)       //subtracting 123 from key2 (key1) comparing to 0
    {
        return 13555;        //return 13555 if key2 (key1) = 0
    }
    return 12;     
}

int main(void) 
{
    char key1[20];
    printf("Enter Key: ");
    fgets(key1,20,stdin);
    strtok(key1, "\n");
    if (firstKey(key1)==13555)
    {
        printf("Success!!.\n");
	    Sleep(5000);
		return 0;
    }
    else
    {
        printf("Failed!!.\n", key1);
	    Sleep(5000);
		return 0;
    }
}
```
