# Lecture 9 | Running a Program
## Interpretation vs Translation
### Interpreter
Directly executes a program in the source language.
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729132516.png)
### Translator
Converts a program from the source language to an quaivalent program in another language.
也就是说，翻译器将语言翻译为上图靠右的语言。
## Compiler
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729134847.png" style="zoom: 50%">
使用 GCC 的时候用 -s 参数，生成 .s 文件，也就是编译器的输出，也是汇编器的输入。
该阶段会包含一些伪指令。
```assembly
mv   t1, t2  <=  addi   t1, t2, 0
```
## Assembler
汇编器的输入是 .s 文件，如果用 RISC-V 指令集架构，那就是 RISC-V 汇编语言。输出是 Object Code。
- Reads and Uses Directives
- Replace Pseudo-instructions(伪指令)
- Produce Machine Language
- Creates Object File
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729142943.png)
### Pseudo-instruction Replacement

| Pseudo           | Real                                                                                                                   |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------- |
| mv    t0, t1     | addi   t0, t1, 0                                                                                                       |
| neg   t0, t1     | sub    t0, zero, t1                                                                                                    |
| li       t0, imm | addi   t0, zero, imm                                                                                                   |
| not    t0, t1    | xori    t0, t1, -1                                                                                                     |
| beqz  t0, loop   | beq    t0, zero, loop                                                                                                  |
| la      t0, str  | lui      t0, str\[31:12]<br>addi    t0, t0, str\[11:0]<br>OR<br>auipc   t0, str\[31:12]<br>addi     t0, t0, str\[11:0] |
### Producing Machine Language
在替换伪指令之后，进行 2 次扫描程序，第一次记下所有标签的位置，第二次扫描是，当在分支中看到标签时，此时我们知道所有标签的位置，use label positions to generate code。
### Symbol Table
- Labels: function calling
- Data: anything in the $\textcolor{red}{.data}$ section; variables which may be accessed across files.
## Linker
- Input: Object code files, information tables.
- Output: Executable code
- Combines several object files into a single executable("$\textcolor{orange}{linking}$")
- Enable separate compilation of files
	- Changes to one file do not require recompilation of the whole program.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240729154254.png" style="zoom:50%">
### Resolving References
- Linker knows:
	- Length of each text and data segment
	- Ordering of text and data segments
- Linker assumes first word of first text segment is at address $\textcolor{orange}{0x10000}$ for RV32
- Linker calculates absolute address of each label to be jumped to and each piece of data being referenced
### Static vs Dynamically Linked Libraries
#### Statically-linked 
Library is now part of the **executable**, so if the library updates, we don't get the fix. Includes the entire library even if not all of it will be used. 
函数和数据被编译进一个二进制文件(一般为 .lib)，在编译链接可执行文件时，链接器从这些库中复制这些函数和数据并把他们和应用程序的其他模块组合起来生成可执行文件(.exe)
#### Dynamically Linked Libraries(DLL)
##### Space/time issues
- **+** Storing a program requires less disk space
- **+** Sending a program requires less time
- **+** Executing two programs requires less memory(if they share a library)
- **-** At runtime, there's time overhead to do link
##### Upgrades
- **+** Replacing one file (**libXYZ.so**) upgrades every program that uses library "**XYZ**"
- **-** Having the executable isn't enough anymore. 也就是说如果我们破坏了某个库，而有 20 个程序在使用它，那么他们都不会运行。
## Loader
- Reads executable file's header to determine size of text and data segments 
- Creates new address space for program large enough to hold text and data segments, along with a stack segment
- Copies instructions + data from executable file into the new address space
- Copies arguments passed to the program onto the stack 
- Initializes machine registers
- Jumps to start-up routine that copies program's arguments from stack to registers & sets the PC
