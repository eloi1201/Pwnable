
# GDB commands 

* set disassembly-flavor intel : GDB will use INTEL asssembly style.

```
(gdb) set disassembly-flavor intel
```

* disass main : Disassemble main function

```
(gdb) disass main
Dump of assembler code for function main:
   0x00000000004005bd <+0>:	push   rbp
   0x00000000004005be <+1>:	mov    rbp,rsp
   0x00000000004005c1 <+4>:	sub    rsp,0x10
   0x00000000004005c5 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x00000000004005c8 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x00000000004005cc <+15>:	cmp    DWORD PTR [rbp-0x4],0x2
   0x00000000004005d0 <+19>:	jne    0x400623 <main+102>
   0x00000000004005d2 <+21>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005d6 <+25>:	add    rax,0x8
   0x00000000004005da <+29>:	mov    rax,QWORD PTR [rax]
   0x00000000004005dd <+32>:	mov    rsi,rax
   0x00000000004005e0 <+35>:	mov    edi,0x4006c4
   0x00000000004005e5 <+40>:	mov    eax,0x0
   0x00000000004005ea <+45>:	call   0x400490 <printf@plt>
   0x00000000004005ef <+50>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005f3 <+54>:	add    rax,0x8
   0x00000000004005f7 <+58>:	mov    rax,QWORD PTR [rax]
   0x00000000004005fa <+61>:	mov    esi,0x4006da
   0x00000000004005ff <+66>:	mov    rdi,rax
   0x0000000000400602 <+69>:	call   0x4004b0 <strcmp@plt>
   0x0000000000400607 <+74>:	test   eax,eax
   0x0000000000400609 <+76>:	jne    0x400617 <main+90>
   0x000000000040060b <+78>:	mov    edi,0x4006ea
   0x0000000000400610 <+83>:	call   0x400480 <puts@plt>
   0x0000000000400615 <+88>:	jmp    0x40062d <main+112>
   0x0000000000400617 <+90>:	mov    edi,0x4006fa
   0x000000000040061c <+95>:	call   0x400480 <puts@plt>
   0x0000000000400621 <+100>:	jmp    0x40062d <main+112>
   0x0000000000400623 <+102>:	mov    edi,0x400701
   0x0000000000400628 <+107>:	call   0x400480 <puts@plt>
   0x000000000040062d <+112>:	mov    eax,0x0
   0x0000000000400632 <+117>:	leave  
   0x0000000000400633 <+118>:	ret    
End of assembler dump.
```

* b      : Sets a break point
  * b *[Function]
  * b *[Address]
* info   : Displays information of break points
* delete : Deletes break points

```
(gdb) b *main
Breakpoint 1 at 0x4005bd
(gdb) info b
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x00000000004005bd <main>
(gdb) b *main+8
Breakpoint 2 at 0x4005c5
(gdb) info b
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x00000000004005bd <main>
2       breakpoint     keep y   0x00000000004005c5 <main+8>
(gdb) delete 2
(gdb) info b
Num     Type           Disp Enb Address            What
1       breakpoint     keep y   0x00000000004005bd <main>
(gdb) delete
Delete all breakpoints? (y or n) y
(gdb) b *0x00000000004005bd
Breakpoint 3 at 0x4005bd
(gdb) info b
Num     Type           Disp Enb Address            What
3       breakpoint     keep y   0x00000000004005bd <main>
(gdb) delete
Delete all breakpoints? (y or n) y
```

* run (or r)  : Starts executing a new instance of a program under GDB.
* cont (or c) : Continues program execution after a breakpoint.
* ni          : Executes one instruction.

```
(gdb) run
Starting program: /root/Desktop/license_1 
Usage: <key>
[Inferior 1 (process 2482) exited normally]
(gdb) run 1234
Starting program: /root/Desktop/license_1 1234
Checking License: 1234
WRONG!
[Inferior 1 (process 2486) exited normally]
(gdb) b *main
Breakpoint 4 at 0x4005bd
(gdb) run
Starting program: /root/Desktop/license_1 1234

Breakpoint 4, 0x00000000004005bd in main ()
(gdb) disass main
Dump of assembler code for function main:
=> 0x00000000004005bd <+0>:	push   rbp
   0x00000000004005be <+1>:	mov    rbp,rsp
   0x00000000004005c1 <+4>:	sub    rsp,0x10
   0x00000000004005c5 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x00000000004005c8 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x00000000004005cc <+15>:	cmp    DWORD PTR [rbp-0x4],0x2
   0x00000000004005d0 <+19>:	jne    0x400623 <main+102>
   0x00000000004005d2 <+21>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005d6 <+25>:	add    rax,0x8
   0x00000000004005da <+29>:	mov    rax,QWORD PTR [rax]
   0x00000000004005dd <+32>:	mov    rsi,rax
   0x00000000004005e0 <+35>:	mov    edi,0x4006c4
   0x00000000004005e5 <+40>:	mov    eax,0x0
   0x00000000004005ea <+45>:	call   0x400490 <printf@plt>
   0x00000000004005ef <+50>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005f3 <+54>:	add    rax,0x8
   0x00000000004005f7 <+58>:	mov    rax,QWORD PTR [rax]
   0x00000000004005fa <+61>:	mov    esi,0x4006da
   0x00000000004005ff <+66>:	mov    rdi,rax
   0x0000000000400602 <+69>:	call   0x4004b0 <strcmp@plt>
   0x0000000000400607 <+74>:	test   eax,eax
   0x0000000000400609 <+76>:	jne    0x400617 <main+90>
   0x000000000040060b <+78>:	mov    edi,0x4006ea
   0x0000000000400610 <+83>:	call   0x400480 <puts@plt>
   0x0000000000400615 <+88>:	jmp    0x40062d <main+112>
   0x0000000000400617 <+90>:	mov    edi,0x4006fa
   0x000000000040061c <+95>:	call   0x400480 <puts@plt>
   0x0000000000400621 <+100>:	jmp    0x40062d <main+112>
   0x0000000000400623 <+102>:	mov    edi,0x400701
   0x0000000000400628 <+107>:	call   0x400480 <puts@plt>
   0x000000000040062d <+112>:	mov    eax,0x0
   0x0000000000400632 <+117>:	leave  
   0x0000000000400633 <+118>:	ret    
End of assembler dump.
(gdb) cont
Continuing.
Checking License: 1234
WRONG!
[Inferior 1 (process 2487) exited normally]
(gdb) run
Starting program: /root/Desktop/license_1 1234
Breakpoint 4, 0x00000000004005bd in main ()
(gdb) ni
0x00000000004005be in main ()
(gdb) disass main
Dump of assembler code for function main:
   0x00000000004005bd <+0>:	push   rbp
=> 0x00000000004005be <+1>:	mov    rbp,rsp
   0x00000000004005c1 <+4>:	sub    rsp,0x10
   0x00000000004005c5 <+8>:	mov    DWORD PTR [rbp-0x4],edi
   0x00000000004005c8 <+11>:	mov    QWORD PTR [rbp-0x10],rsi
   0x00000000004005cc <+15>:	cmp    DWORD PTR [rbp-0x4],0x2
   0x00000000004005d0 <+19>:	jne    0x400623 <main+102>
   0x00000000004005d2 <+21>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005d6 <+25>:	add    rax,0x8
   0x00000000004005da <+29>:	mov    rax,QWORD PTR [rax]
   0x00000000004005dd <+32>:	mov    rsi,rax
   0x00000000004005e0 <+35>:	mov    edi,0x4006c4
   0x00000000004005e5 <+40>:	mov    eax,0x0
   0x00000000004005ea <+45>:	call   0x400490 <printf@plt>
   0x00000000004005ef <+50>:	mov    rax,QWORD PTR [rbp-0x10]
   0x00000000004005f3 <+54>:	add    rax,0x8
   0x00000000004005f7 <+58>:	mov    rax,QWORD PTR [rax]
   0x00000000004005fa <+61>:	mov    esi,0x4006da
   0x00000000004005ff <+66>:	mov    rdi,rax
   0x0000000000400602 <+69>:	call   0x4004b0 <strcmp@plt>
   0x0000000000400607 <+74>:	test   eax,eax
   0x0000000000400609 <+76>:	jne    0x400617 <main+90>
   0x000000000040060b <+78>:	mov    edi,0x4006ea
   0x0000000000400610 <+83>:	call   0x400480 <puts@plt>
   0x0000000000400615 <+88>:	jmp    0x40062d <main+112>
   0x0000000000400617 <+90>:	mov    edi,0x4006fa
   0x000000000040061c <+95>:	call   0x400480 <puts@plt>
   0x0000000000400621 <+100>:	jmp    0x40062d <main+112>
   0x0000000000400623 <+102>:	mov    edi,0x400701
   0x0000000000400628 <+107>:	call   0x400480 <puts@plt>
   0x000000000040062d <+112>:	mov    eax,0x0
   0x0000000000400632 <+117>:	leave  
   0x0000000000400633 <+118>:	ret    
End of assembler dump.
```

* info reg   : Displays registers information
* info break : Displays break points
* x/x        : Displays memory address with hexdecimal
  * x/bx : Dispalys 1 byte
  * x/hx : Dispalys 2 bytes
  * x/dx : Dispalys 4 bytes
  * x/gx : Dispalys 8 bytes

```
(gdb) info reg
rax            0x4005bd            4195773
rbx            0x0                 0
rcx            0x7ffff7fa6718      140737353770776
rdx            0x7fffffffe2b0      140737488347824
rsi            0x7fffffffe298      140737488347800
rdi            0x2                 2
rbp            0x400640            0x400640 <__libc_csu_init>
rsp            0x7fffffffe1b0      0x7fffffffe1b0
r8             0x7ffff7fa7d80      140737353776512
r9             0x7ffff7fa7d80      140737353776512
r10            0x89b               2203
r11            0x7ffff7e11a30      140737352112688
r12            0x4004d0            4195536
r13            0x7fffffffe290      140737488347792
r14            0x0                 0
r15            0x0                 0
rip            0x4005be            0x4005be <main+1>
eflags         0x246               [ PF ZF IF ]
cs             0x33                51
ss             0x2b                43
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
(gdb) info reg $rsp
rsp            0x7fffffffe1b0      0x7fffffffe1b0
(gdb) x/x $rsp
0x7fffffffe1b0:	0x00400640
(gdb) x/c $rsp
0x7fffffffe1b0:	64 '@'
(gdb) x/s $rsp
0x7fffffffe1b0:	"@\006@"
(gdb) x/xs $rsp
0x7fffffffe1b0:	"@\006@"
(gdb) x/gx $rsp
0x7fffffffe1b0:	0x0000000000400640
(gdb) x/10gx $rsp
0x7fffffffe1b0:	0x0000000000400640	0x00007ffff7e11b17
0x7fffffffe1c0:	0x0000000000000000	0x00007fffffffe298
0x7fffffffe1d0:	0x0000000200000000	0x00000000004005bd
0x7fffffffe1e0:	0x0000000000000000	0x144f4e80aa7034f2
0x7fffffffe1f0:	0x00000000004004d0	0x00007fffffffe290
(gdb) 
```
