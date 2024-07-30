# Lecture 8 
## R-Format Layout
在 RISC-V 中, 1 word = 4 Bytes = 32 bits.
将 32 位指令分为不同段
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726145032.png)
其中 opcode 为操作码，所有 R 类型寄存器的操作码都是 $0110011_2$ 
rs1 和 rs2 为源寄存器，rd 为目标寄存器

对于
```assembly
add   x18, x19, x10
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726150021.png)

```assembly
add   x4, x3, x2
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726150229.png)
则指令的正确编码为 $0021~ ~8233_{16}$
### All RV32 R-format instructions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726150829.png)
## I-Format Layout
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726151405.png)
imm\[11:0] 存储立即数，从 $-2048_{10} \sim +2047_{10}$
```assembly
addi   x15, x1, -50
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726151835.png)
### All RV32 I-format instructions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726152113.png)
## RISC-V Loads
Load Instructions 延用 I-Format Layout
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726152931.png)
```assembly
lw   x14, 8(x2)
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726153117.png)
### All RV32 Loads instructions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726153237.png)
其中，lbu 和 lhu 不执行符号扩展。
## S-Format Layout
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726153413.png)
rs1 for base memory address, rs2 for data to be stored.
```assembly
sw   x14, 8(x2)
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726153743.png)
### All RV32 S-format instructions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726153835.png)
## B-Format Layout
如果不执行分支
```
PC = PC + 4
```
RISC-V 支持半字对齐，如果是 32 位 RISC-V 指令的任何给定字节地址 X，下一条指令将在内存中的地址 X + 4 处开始。如果使用 16 位的压缩指令时，PC 递增 2。
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240726160922.png)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729110543.png)
### All RISC-V Branch instructions
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729105759.png)
## U-Format Layout
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729111919.png)
lui: Load Upper Immediate
auipc: Add Upper Immediate to PC
### LUI
LUI 会将立即数值写入目标寄存器的最高 20 位，并将最低 20 位清零。例如对于 0x87654321
```assembly
lui   x10, 0x87654       # x10 = 0x87654000
addi  x10, x10, 0x321    # x10 = 0x87654321
```
但是对于
```assembly
lui   x10, 0xDEADB       # x10 = 0xDEADB000
addi  x10, x10, 0xEEF    # x10 = 0xDEADAEEF
```
对于 addi，它会进行符号位拓展，对于 0xEEF，由于最高位是 1，则前面 5 个半字节都会被扩展为 1。相当于对 0xDEADB 进行减 1。也就变成了 0xDEADA。
所以这种方法被淘汰了。解决方案就是直接使用指令 li。它会帮我们处理好。(Pre-increment value placed in upper 20 bits, if sign bit will be set on immediate in lower 12 bits.)
```assembly
li   x10, 0xDEADBEEF
```
### AUIPC
Adds upper immediate value to PC and places result in destination register. Used for PC-relative addressing.
```assembly
Label:  AUIPC   x10, 0   # Puts address of Label in x10
```
## J-Format Layout
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729115241.png)
jal saves PC + 4 in register rd(the return address). The way not to save the return address is to specify the rd as x0, which would discard the value stored there.
```assembly
j Label = jal x0, Label  # Discard return address

jal ra, FuncName 
```
## JALR Instruction (I-Format)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729115416.png)
```assembly
jalr   rd, rs, immediate
```
