## 安装 $ccache$
$ccache~ - ~a ~fast ~C/C++ ~compiler ~cache$
> It [speeds up recompilation](https://ccache.dev/performance.html) by caching previous compilations and detecting when the same compilation is being done again.

$which$ 命令可以搜索 $PATH 环境变量中的路径列表，并输出指定为参数的命令的完整路径。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240327201542.png)
他只有一个可选参数 $-a$，用于指示它打印所有匹配项
通过以下指令获得的默认路径为 /usr/bin/gcc
```shell
which gcc
```

安装 $ccache$
```shell
sudo apt-get install ccache
```
我们需要阅读 $man~ccache$ 中的手册，来将 /usr/bin/gcc 改为 /usr/lib/ccache/gcc
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240327203122.png)
手册提示我们需要将 /usr/lib/ccache 添加到我们的环境变量中。
```shell
vim ~/.bashrc
```
在最下方一行添加 
```shell
export PATH="/usr/lib/ccache:$PATH"
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240327203645.png)

再保存退出。
输入
```shell
source ~/.bashrc
```
使其生效。此时再输入
```shell
which gcc
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240327203757.png)
发现 gcc 的路径已经发生了变化。

在 /am-kernels/tests/am-tests 目录下。清除原先的编译结果，再次编译。并用 time 测量时间。
```shell
make clean
time make ARCH=native mainargs=k run
```
发现编译时间反而比之前慢了。
> 这是因为除了需要开展正常的编译工作之外, `ccache`还需要花时间把目标文件存起来. 接下来再次清除编辑结果, 重新编译并统计时间, 你会发现第二次编译的速度有了非常明显的提升! 这说明`ccache`确实跳过了完全重复的编译过程, 发挥了加速的作用. 如果和多线程编译共同使用, 编译速度还能进一步加快!
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240327204015.png)

再次清除编译结果，然后进行编译。发现速度变快了许多。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240327203945.png)


## ISA 指令集架构
> In [computer science](https://en.wikipedia.org/wiki/Computer_science "Computer science"), an **instruction set architecture** (**ISA**) is a part of the [abstract model](https://en.wikipedia.org/wiki/Abstract_model) of a [computer](https://en.wikipedia.org/wiki/Computer "Computer"), which generally defines how software controls the CPU.[[1]](https://en.wikipedia.org/wiki/Instruction_set_architecture#cite_note-1) A device that executes instructions described by that ISA, such as a [central processing unit](https://en.wikipedia.org/wiki/Central_processing_unit "Central processing unit") (CPU), is called an _implementation_.

ISA 类似于一种规范：
如果一个程序要在特定架构的计算机上运行, 那么这个程序和计算机就必须是符合同一套规范才行。

$x86$
$riscv32(64)$
$mips32$

## man
CR 代表回车
```shell
man -k printf
```
可以打印出所有候选参数
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240327214512.png)
再通过
```shell
man 3 printf
```
可以查看它的 manual page


将计算机看成是一个先驱制造的。先驱制造计算机，首先需要程序的存储位置，而这个存储部件需要存储足够大容量来放下各种各样的程序，他就是存储器。先驱制造存储器并且把程序放在存储器中等待CPU执行。


$MakeFile$
$\$@$:
> 	The file name of the target of the rule. If the target is an archive member, then ‘$@’ is the name of the archive file. In a pattern rule that has multiple targets (see [Introduction to Pattern Rules](https://www.gnu.org/software/make/manual/html_node/Pattern-Intro.html)), ‘$@’ is the name of whichever target caused the rule’s recipe to be run.
$\$<$
> 	The name of the first prerequisite. If the target got its recipe from an implicit rule, this will be the first prerequisite added by the implicit rule (see [Using Implicit Rules](https://www.gnu.org/software/make/manual/html_node/Implicit-Rules.html)).


接下来就是让笔者最痛苦的阅读源码环节（C语言基础不是特别好）。至少阅读几个“简单的”初始化函数也需要花费大量时间。
### $parse\_agrs$
$getopt$ 获取命令
"ab:c" 是 optstring。: 代表需要一个参数，:: 代表可选的参数。
"a:b:c:" 代表 a, b, c 都需要一个参数。
```cpp
/* getopt */
#include <unistd.h>
extern char *optarg;
extern int optind;
extern int optopt;
extern int opterr;
extern int optreset;
int getopt(int argc, char * const *argv, const char *optstring);
```

```c
/* getopt.c */
#include <unistd.h>
#include <stdio.h>
int main(int argc, char * argv[])
{
    int aflag=0, bflag=0, cflag=0;
    int ch;
    while ((ch = getopt(argc, argv, "ab:c")) != -1)
    {
        printf("optind: %d\n", optind);
        switch (ch) {
        case 'a':
            printf("HAVE option: -a\n");
            aflag = 1;
            break;
        case 'b':
            printf("HAVE option: -b\n");
            bflag = 1;
            printf("The argument of -b is %s\n", optarg);
            break;
        case 'c':
            printf("HAVE option: -c");
            cflag = 1;
            break;
        case '?':
            printf("Unknown option: %c\n",(char)optopt);
            break;
        }
    }
}
```
运行效果如图：
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240328205948.png)
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240328210011.png)
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240328210033.png)

$getopt\_long$ 获取长参数
```c
const struct option table[] = {
    {"batch"    , no_argument      , NULL, 'b'},
    {"log"      , required_argument, NULL, 'l'},
    {"diff"     , required_argument, NULL, 'd'},
    {"port"     , required_argument, NULL, 'p'},
    {"help"     , no_argument      , NULL, 'h'},
    {0          , 0                , NULL,  0 },
  };
```
对于 option 
```cpp
struct option{
      const char *name;
      int has_arg;
      int *flag;
      int val;
 };
```
如果 flag 为 NULL,  getopt_long() 返回 val 中数值。

--batch -> -b

### $init\_rand()$
```c
void init_rand() {
  srand(MUXDEF(CONFIG_TARGET_AM, 0, time(0)));
}
```
time() 参数为 0 或者 NULL 是取系统时间
```c
/* nemu>include>common.h */
typedef MUXDEF(CONFIG_ISA64, uint64_t, uint32_t) word_t;
typedef MUXDEF(CONFIG_ISA64, int64_t, int32_t)  sword_t;
```

### $init\_log(log\_file)$
```c
void init_log(const char *log_file) {
  log_fp = stdout;
  if (log_file != NULL) {
    FILE *fp = fopen(log_file, "w");
    Assert(fp, "Can not open '%s'", log_file);
    log_fp = fp;
  }
  Log("Log is written to %s", log_file ? log_file : "stdout");
}
```
stdout 定义在 <stdio.h> 中
```c
/* Standard streams.  */
extern FILE *stdin;		/* Standard input stream.  */
extern FILE *stdout;		/* Standard output stream.  */
extern FILE *stderr;		/* Standard error output stream.  */
/* C89/C99 say they're macros.  Make them happy.  */
#define stdin stdin
#define stdout stdout
#define stderr stderr
```
stdout 相当于是向屏幕输出，默认行缓冲，遇到 $\n$ 才会输出
[fflush stdin stdout stderr](https://blog.csdn.net/tonglin12138/article/details/85546563)

$init\_mem()$
个人注释：
```c
void init_mem() {
#if   defined(CONFIG_PMEM_MALLOC)
  pmem = malloc(CONFIG_MSIZE);  // 给 memory 分配空间
  assert(pmem); 
#endif
#ifdef CONFIG_MEM_RANDOM
  uint32_t *p = (uint32_t *)pmem; // p 指针指向 memory 所在位置
  int i;
  for (i = 0; i < (int) (CONFIG_MSIZE / sizeof(p[0])); i ++) {
    p[i] = rand(); // 随机分配 memory 物理地址？
  }
#endif
  Log("physical memory area [" FMT_PADDR ", " FMT_PADDR "]", PMEM_LEFT, PMEM_RIGHT);
}
```
为什么 pmem 为 uint8_t 要转化为 uint32_t ?
chatgpt 的回答：
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240328214557.png)

运行 make run 报错
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240328222121.png)
PA0 提示实在 nemu\src\monitor\monitor.c 的 36 行触发了断言错误
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240328230521.png)
将 Log 和 assert 两行注释掉。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240328230657.png)
我们再进行 make run
发现错误提示消失。


```c
void cpu_exec(uint64_t n)
```

### $Q$ 向 $cpu\_exec$ 函数传入参数 $-1$ 是什么意思
uint64_t 是 64 位无符号整数
$uint64\_t.min=0$
$uint64\_t.max=18446744073709551615$
如果传入 $-1$，相当于在有符号的情况下二进制数全为 $1$。因此，他表示无符号的 $uint64\_t$ 的最大值。
传入 $-1$ 是想让它近乎无限执行下去???

### 用 GDB 调试 NEMU
进入 gdb 调试界面
```shell
make gdb
```
在 gdb 界面输入以下指令进入图形化界面
```shell
layout split
```
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402165255.png)
#### GDB常用指令
```shell
b main   // 在 main 函数处添加断点
run [args] // 运行程序 run 123
s        // 进入程序
n        // 执行下一行
c        // 继续程序
p 变量名  // 打印变量，也可以是表达式 p 1+2
info locals // 查看当前函数里的所有变量对应的值
quit     // 退出 gdb
```

### 为 NEMU 编译添加 GDB 调试信息
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240401213259.png)

![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240401213334.png)

### 实现优美的退出
> 为了测试大家是否已经理解框架代码, 我们给大家设置一个练习: 如果在运行NEMU之后直接键入`q`退出, 你会发现终端输出了一些错误信息. 请分析这个错误信息是什么原因造成的, 然后尝试在NEMU中修复它.
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240401213642.png)


我们看 nemu_main.c 中的主函数
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402162033.png)
engine_start() 函数
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402162912.png)
sdb_mainloop() 可以接收用户的指令。

sdb.c 中
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402161657.png)
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402161856.png)
在 sdb_mainloop() 中有这么一段。可以发现如果键入 q，那么会 return(cmd_q() 返回 -1)
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402161745.png)

sdb_mainloop() 执行完之后， return 
进入 is_exit_status_bad()
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402163247.png)
如果 good == 1，则程序正常退出。如果为 0，则程序错误退出。

当然，如果打开 gdb 进行调试
发现如果直接在 nemu 界面输入 q。
程序会到 return is_exit_status_bad();
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402172550.png)


所以需要让 nemu_state.state = NEMU_QUIT。那么我们在输入为 q 键的时候让这个条件成立。
在 cmd_q() 函数下添加
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402164903.png)
再次 make run
输入 q 发现不会报错。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402165009.png)

## $strtok()$
[原文链接](https://www.runoob.com/cprogramming/c-function-strtok.html)
函数声明：
```c
char *strtok(char *str, const char *delim)
```
str 代表要被分解成一组小字符串的字符串，delim 是包含分隔符的字符串
(分割处理后原字符串 str 的分隔符会变成 '\0')

在 cmd_help 函数中我们看到一行
```c
char *arg = strtok(NULL, " ");
```
stackoverflow 上 [why-do-we-use-null-in-strtok](https://stackoverflow.com/questions/23456374/why-do-we-use-null-in-strtok)
他可以从上一次调用中未处理的字符串中继续查找

## $sscanf()$
[原文链接](https://www.runoob.com/cprogramming/c-function-sscanf.html)
函数声明
```c
int sscanf(const char *str, const char *format, ...)
```

# 基础设施
## 单步执行 $si~[N]$
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402194422.png)
在 cmd_table[] 里加上一行 
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402195653.png)
对于 cmd_si 函数的声明。由于如果缺参数，默认设置为 0，所以如果 args == NULL，那么令需要执行的指令数 n 为 1。否则用 sscanf 读取并存储到 n 变量中。使用 cpu_exec() 函数进行执行。
```c
static int cmd_si(char *args) {
  int n;
  if(args == NULL) {
    n = 1;
  }
  else {
    sscanf(args, "%d", &n);
  }
  cpu_exec(n);
  return 0;
}
```
在 risc32 中，指令长度为 4Byte
执行一次，地址偏移 4Byte
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402200619.png)

## 打印程序状态
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240402201744.png)
在 cmd_table[] 中添加
```c
{"info", "Print the state of program", cmd_info}
```
再创建函数 cmd_info(char \*args)

在 gdb 的图形化界面可以打印程序寄存器状态(运行时)
```gdb
info registers
```
或者用简写命令 "i r"

也可以用
```gdb
layout regs
```
展示寄存器的图形化界面

以下是 x86-64 架构下的寄存器和他对应的值。 0x 开头为 16 进制表示，最后一列为十进制表示。
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409211934.png)
在 riscv-32 中定义了
![image.png](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240409212105.png)
%#x 可以打印以 0x 开头的 16 进制数。
```c
void isa_reg_display() {
  int length = ARRLEN(regs); // 获取数组的长度

  for(int i = 0; i < length; i ++) {
    printf("%-8s%-#20x%-20u\n", regs[i], cpu.gpr[i], cpu.gpr[i]);
  }
}
```