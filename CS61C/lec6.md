# Lecture 6
## 主流 ISA
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613233121.png)
## Register
汇编语言没有变量。它用寄存器来存储值。
寄存器是固定大小的小内存(32 位或者 64 位)。可以进行读取和写入，但是有数量限制，它们很快并且耗电少。
### Registers vs. Memory
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613234920.png)

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613234822.png)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613234838.png" style="zoom:50%">

#### What if more variables than registers?
如果变量多于寄存器数量，我们选择将最常用的变量存储到寄存器中，然后将其余的存储到内存中。(称为 spilling to memory)
#### Why are not all variables in memory?
寄存器比内存快 100-500 倍。
## Locality Memory Hierarchy
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240613235158.png)
## RISCV
RISC V 有 32 个寄存器，从 x0 到 x31。
每个寄存器都是 32 bits wide and holds a word(a fixed size piece of data that handles as a unit by the instruction set or hardware of the processor, a word is defined as the size of a CPU's registers).
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614000646.png)
s 开头的寄存器称为 safe registers，它们用来保存编程变量。
t 开头的寄存器持有临时变量。
### The Zero Register
x0(zero) 永远有值 0 并且不能被改变！任何对 x0 寄存器的写入操作都无效。
## Registers in a Computer
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614001134.png" style="zoom:70%">
## RISCV Instructions
```assembly
op dst, src1, src2
```
op: operation name
dst: register getting result
src1: first register for operation
src2: second register for operation

汇编指令和 C 相关(=, +, -, \*, /, \&, |, etc)
```assembly
main: add    t0, x0, x0
    # op   dst1 src1 src2
    # 将 x0 和 x0 寄存器内容相加，结果存入 t0 寄存器中
```
### Integer Addition(add)
在 C 语言中:
```c
a = b + c;
```
在 RISCV 中:
```assembly
add  s1, s2, s3     # s1 = a
```
### Integer Subtraction(sub)
在 C 语言中:
```c
a = b - c;
```
在 RISCV 中:
```assembly
sub  s1, s2, s3    # s1 = a, s2 = b, s3 = c
```
### RISCV Instructions Example
假设 a -> s0, b -> s1, c -> s2, d -> s3, e -> s4。将 a = (b + c) - (d + e) 转换为 RISCV。其中，t1 和 t2 是存储临时变量的寄存器。
```assembly
add t1, s1, s2         # t1 = b + c
add t2, s3, s4         # t2 = d + e
sub s0, t1, t2         # s0 = t1 - t2 = (b + c) - (d + e)
```
### Immediates
Immediates: Numerical constants
```assembly
opi dst, src, imm
```
操作的名称结尾加个 'i'。
Immediates 可以达到 12 bits
```assembly
addi s1, s2, 5    # a = b + 5
addi s3, s3, 1    # c 存储在 s3 中，相当于 c ++
```
假设 a -> s0, b -> s1, 将 a = (5 + b) - 3; 转换为 RISCV
```assembly
addi t1, s1, 5     # t1 = 5 + b
addi s0, t1, -3    # a = t1 - 3
```
## Data Transfer
Data Transfer instructions are between registers(Datapath) and Memory. Allow us to fetch and store operands in memory.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614103457.png" style="zoom:70%">
```assembly
memop reg, off(bAddr)
```
- **memop**: operation name("operator")
- **reg**: register for operation source or destination
- **bAddr**: register with pointer to memory("base address")
- **off**: address offset(immediate) in bytes("offset")
Access memory at address $bAddr + off$
### Memory is Byte-Addressed
不同系统下 word 和 Byte 和 bit 的关系

| 系统  |   字    |   字节    |    位    |
| :-: | :----: | :-----: | :-----: |
| 16位 | 1 word | 2 Bytes | 16 bits |
| 32位 | 1 word | 4 Bytes | 32 bits |
| 64位 | 1 word | 8 Bytes | 64 bits |
Memory addresses 由 byte 而不是 word 来索引
Word addresses 每个相隔 4 Bytes(32 位系统下)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614105220.png" style="zoom: 50%">
## Data Transfer Instructions
#### Load Word(lw)
-Takes data at address $bAddr + off$ **FROM** **memory** and places it into **reg**.
#### Store Word(sw)
-Takes data in **reg** and stores it **TO** **memory** at address $bAddr + off$
#### example
address of int array\[] -> s3, value of b -> s2, 
```c
array[10] = array[3] + b;
```
转换成 RISCV
```assembly
lw  t0, 12(s3)    # t0 = A[3]
add t0, s2, t0    # t0 = A[3] + b
sw  t0, 40(s3)    # A[10] = A[3] + b
```
## Values can start off in memory
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614110443.png" style="zoom: 50%">
$.data$ 指定了数据的存储位置。
$.text$ 指定了代码的存储位置。
## Endianness
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614110901.png)
**RISC-V 是 Little Endian**
## Sign Extension
### Sign Extend
Take the most-significant bit and copy it to the new bits
$$
0b~~11 = 0b~~1111
$$
### Zero/One Pad
Set the new bits with one/zero.
$$
\begin{aligned}
Zero~~Pad:&0b~~11 = 0b~~0011 \\
One~~Pad:&0b~~11 = 0b~~1111
\end{aligned}
$$
**RSIC-V 是 Sign extend**
## Byte Instructions
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614111441.png" style="zoom:70%">
$s0 = 0x00000180$
```assembly
lb s1, 1(s0)  # 获得 1 个字节，也就是 0x01，s1 = 0x00000001
lb s2, 0(s0)  # 获取 0x80，s2 = 0xFFFFFF80
sb s2, 2(s0)  # 从 s2 中取出最低 1 个字节，存储到 s0 第 3 个 字节的位置，*(s0) = 0x00800180
```
## Half-Word Instructions
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614112126.png" style=“zoom: 70%”>
## Unsigned Instructions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614114516.png)
意味着当加载指令时，用 **0** 进行填充而非 sign extending。
## Data Transfer Greencard Explanation
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614114818.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614114821.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240614114922.png)
## Decision Making Instructions
### Branch If Equal(beq)
If value in reg1 = value in reg2, go to label
Otherwise go to the next instruction
```assembly
beq reg1, reg2, label
```
### Branch If Not Equal(bne)\
If value in reg $\neq$ value in reg2, go to label
```assembly
bne reg1, reg2, label
```
### Jump(j)
Unconditional jump to label
```assembly
j label
```
### Branching On Conditions other than (Not) Equal
#### Branch Less Than(blt)
If value in reg1 < value in reg2, go to label
```assembly
blt reg1, reg2, label
```
#### Branch Greater Than or Equal(bge)
If value in reg1 >= value in reg2, go to label
```assembly
bge reg1, reg2, label
```
### If-Else
C 语言代码:
```c
if(i == j) 
	a = b;  /* then */
else
	a = -b; /* else */
```
RISC-V 代码:
```assembly
# i -> s0, j -> s1
# a -> s2, b -> s3

beq s0, s1, then
else:
sub s2, s3, x0   # x0 = 0, s2 = s3 - 0 -> a = b - 0 = b
j end
else:
sub s2, x0, s3   # x0 = 0, s2 = 0 - s3 -> a = 0 - b = -b
end:
```

C 语言代码
```c
if(i < j) 
	a = b;   /* then */
else
	a = -b;  /* else */
```
RISC-V 代码:
```assembly
# i -> s0, j -> s1
# a -> s2, b -> s3

bge s0, s1, else
then:
add s2, s3, x0
j end
else: 
sub s2, x0, s3
end:
```
## Instruction Addresses
指令作为数据存储在 memory 中并且有自己的地址。
Labels 会被转换为指令地址。
PC 会跟踪 CPU 当前执行的指令。
## Control Flow Greencard Explanation
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240616000826.png" style="70%">
imm 的第 0 位是 0，来保证它是偶数，这样 PC 的值总是会半对齐。
## Shifting Instructions 
**Logical shift**：Add zeros as shift
**Arithmetic shift**: Sign-extend as you shift，只对右移有效。
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240616003241.png" style="zoom: 70%">

<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240616003848.png" style="zoom: 50%">

以下代码将 s1 的值存储到 s0 地址的第4个字节（最高字节）
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240616013651.png" style="zoom: 50%">
假设 **s0: 0x12345678**。**s1: 0xAB**
**lw t0, 0(s0)** 从 s0 地址读取当前值 0x12345678 到寄存器 t0，t0 = '0x12345678'。
**li t1, 0x00FFFFFF** 将立即数 0x00FFFFFF 加载到寄存器 t1。t1 = 0x00FFFFFF。
**and t0, t0, t1** 将 t0 与 t1 按位与，清除 t0 的最高字节。t0 = '0x12345678' & '0x00FFFFFF'，最终 t0 = '0x00345678'(最高字节已经清零)
**slli t1, s1, 24** 将 s1 的值左移 24 位，将其移动到最高字节位置，也就是 0xAB << 24 -> t1 = 0xAB000000
**or t0, t0, t1** 将 t0 和 t1 按位或操作，合并新的最高字节。t0 = 0x00345678 | 0xAB000000，t0 = '0xAB345678'
**sw t0, 0(s0)** 将 t0 的值 0xAB345678 存储回 s0 地址，s0 = 0xAB345678
## Arithmetic Instructions Myltiply Extension
### Multiplication(mul and mulh)
$src1 \times src2$：lower 32-bits through mul, upper 32-bits in mulh
```assembly
mul dst, src1, src2
mulh dst, src1, src2
```
### Division(div)
src1 / src2: quotient via div, remainder via rem
```assembly
div dst, src1, src2
rem dst, src1, src2
```
## Bitwise Instructions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240616014841.png)
## Compare Instructions
### Set Less Than (slt)
If value in reg1 < value in reg2, dst = 1, else 0
```assembly
slt dst, reg1, reg2
```
### Set Less Than Immediate (slti)
If value in reg1 < imm, dst = 1, else 0
```assembly
slti dst, reg1, imm
```
