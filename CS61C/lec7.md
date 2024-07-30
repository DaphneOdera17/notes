# Lecture 7
## Change C language To RISC-V
### Ex.1
```c
char *p, *q;
while((*q++ = *p ++) != '\0');
```

```
p->s0, q->s1
t0 = *p
*q = t0
p = p + 1
q = q + 1
if *p == 0, go to Exit
go to Loop
```

```assembly
Loop: lb    t0, 0(s0)
	  sb    t0, 0(s1)
	  addi  s0, s0, 1
	  addi  s1, s1, 1
	  beq   t0, x0, Exit
	  j     Loop
Exit:
```
### Ex.2
```c
int A[20];
int sum = 0;
for(int i = 0; i < 20; i ++) 
	sum += A[i];
```

```assembly
	add   x9, x8, x0     # x9 = &A[0]
	add   x10, x0, x0    # sum
	add   x11, x0, x0    # i
	addi  x13, x0, 20    # x13
Loop:
	bge   x11, x13, Done
	lw    x12, 0(x9)     # x12 A[i]
	add   x10, x10, x12  # sum
	addi  x9, x9, 4      # &A[i + 1]
	addi  x11, x11, 1    # i ++
	j Loop
Done:
```
## 一些更短的指令
```assembly
mv rd, rs = addi rd, rs, 0
li rd, 13 = addi rd, x0, 13
nop       = addi x0, x0, 0    # 无操作
```
## Functions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240725184244.png)
### jump register(jr)
```assembly
address (shown in decimal)
1000 mv a0, s0           # x = a
1004 mv a1, s1           # y = b
1008 addi ra, zero, 1016 # ra = 1016
1012 j sum               # jump to sum
1016 ...
...
2000 sum: add a0, a0, a1
2004 jr ra
```
以上代码为什么使用 jr 而不是 j 是因为 sum 函数可能会在很多地方被调用，我们无法返回到一个固定的位置，所以必须要用 jr 来指定返回的位置。
### jump and link(jal)
Single instruction to jump and save return address.
```assembly
# Before
1008 addi ra, zero, 1016  # ra = 1016
1012 j sum                # goto sum

# After
1008 jal sum # ra = 1012, goto sum
```

```
jal  rd, Label   jump and link
jalr 
```
### 函数调用的一些步骤
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240725193127.png)

```c
int Leaf(int g, int h, int i, int j)
{
	int f;
	f = (g + h) - (i + j);
	return f;
}
```
g, h, i, j 分别存储在 a0, a1, a2, a3
f 存储在 s0
我们需要在调用函数之前存储旧的值，由于我们通常没有足够的寄存器来处理每个函数调用，所以将它们存储在内存中的 stack(LIFO)。
Stack 有两个操作:
Push: placing data onto stack
Pop: removing data from stack

由于 Stack 在内存中，所以需要有寄存器来指向它，也就是 sp(stack pointer)，在 RISC-V 中，存储在 **x2** 寄存器中。
#### Stack frame
堆栈帧包含：
1.Return "instruction" address
2.Parameters (arguments)
3.Space for other local variables

```assembly
Leaf:   
		# prologue
		addi sp, sp, -8  # adjust stack for 2 items
		sw   s1, 4(sp)   # save s1 for use afterwards
		sw   s0, 0(sp)   # save s0 for use afterwards

		add  s0, a0, a1  # f = g + h
		add  s1, a2, a3  # s1 = i + j
		sub  a0, s0, s1  # return value (g + h) - (i + j)

		# epilogue
		lw   s0, 0(sp)   # restore register s0 for caller
		lw   s1, 4(sp)   # restore register s1 for caller
		addi sp, sp, 8   # adjust stack to delete 2 items
		jr   ra          # jump back to calling routine
```
该函数调用前、中、后栈帧与 sp 变化
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240725212606.png)
Saved registers: s0 - s11
易失性或临时存储器：
Argument/return registers: a0 - a7, ra
Temporary registers: t0 - t6

| Register | ABI Name | Description                         | Saver  |
| -------- | -------- | ----------------------------------- | ------ |
| x0       | zero     | Hard-wired zero                     | -      |
| x1       | ra       | Return address                      | Caller |
| x2       | sp       | Satck pointer                       | Callee |
| x3       | gp       | Global pointer                      | -      |
| x4       | tp       | Thread pointer                      | -      |
| x5       | t0       | Temporary / Alternate link register | Caller |
| x6-7     | t1-2     | Temporaries                         | Caller |
| x8       | s0/fp    | Saved register / Frame pointer      | Callee |
| x9       | s1       | Saved register                      | Callee |
| x10-11   | a0-1     | Function arguments / Return values  | Caller |
| x12-17   | a2-7     | Function arguments                  | Caller |
| x18-27   | s2-11    | Saved registers                     | Callee |
| x28-31   | t3-6     | Temporaries                         | Caller |
其中，Caller 是调用函数，而 Callee 是被调用函数。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240725215732.png)
```c
int sumSquare(int x, int y) {
	return mult(x, x) + y;
}
```

```assembly
sumSquare:
	addi  sp, sp, -8   # space on stack (push)
	sw    ra, 4(sp)    # save ret addr  (push)
	sw    a1, 0(sp)    # save y         (push)
	mv    a1, a0       # mult(x, x)
	jal   mult         # call mult
	lw    a1, 0(sp)    # restore y      (pop)
	add   a0, a0, a1   # mult() + y
	lw    ra, 4(sp)    # get ret addr   (pop)
	addi  sp, sp, 8    # restore stack  (pop)
	jr    ra
```