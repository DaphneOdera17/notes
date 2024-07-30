# Lecture 10 | State registers
## NAND
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730144458.png)


| a   | b   | c   |
| --- | --- | --- |
| 0   | 0   | 1   |
| 0   | 1   | 1   |
| 1   | 0   | 1   |
| 1   | 1   | 0   |
## Signals and Waveforms
### Clock
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730144756.png)
### Grouping
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730145316.png" style="zoom:50%">
### Circuit Delay
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730145354.png" style="zoom:70%">
## Circuits with State(e.g. register)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730151220.png)
## Accumulator
```c
S = 0;
for(i = 0; i < n; i ++)
	S = S + Xi;
```
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730152017.png)
Register is used to hold up the transfer of data to adder.
When reset line is asserted or goes one, the register will be reset.
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730152110.png)
### Register Details Flip-flops
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730152240.png)
一个 n 位寄存器实际上是 n 个 1 位触发器。
D input is **Data**, Q is **output**
这些也叫做 D-type Flip-Flop
#### 上升沿触发(rising edge-triggered)
当它从 0 变为 1 时，就会触发。
On the rising edge of the clock, the input d is sampled and transferred to the output. At all other times, the input d is ignored.
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730152628.png" style="zoom:50%">
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730153000.png)
q 中刚开始的阴影部分代表可能是 1 也可能是 0。红色部分是因为存在一定延迟。
#### Example(more detail)
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730153540.png)
### Accumulator Revisited
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730153936.png)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730153943.png" style="zoom:50%">

![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730154505.png)
- Reset signal shown.
- Also, in practice X might not arrive to the adder at the same time as $S_{i-1}$
- $S_i$ temporarily is wrong(底下阴影部分), but register always captures correct value.
- In good circuits, instability never happens around rising edge of clk.

|                |                                                                                              |
| -------------- | -------------------------------------------------------------------------------------------- |
| **Clock(CLK)** | steady square wave that synchronizes system                                                  |
| **Setup Time** | when the input must be stable before the rising edge of the CLK                              |
| **Hold Time**  | when the input must be stable after the rising edge of the CLK                               |
| **CLK-to-Q**   | Delay -- how long it takes the output to change, measured from<br>the rising edge of the CLK |
| **Flip-flop**  | ont bit of state that samples every rising edge of the CLK                                   |
| **Register**   | several bits of state that samples on rising edge of CLK or on<br>LOAD                       |
## Finite State Machines(FSM) 有限状态机
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730155354.png" style="zoom:50%">
### Example: 3 ones
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730155702.png)
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730155952.png" style="zoom:50%">
#### 流程如图：
![](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730160629.png)
#### Hardware Implementation of FSM
<img src="https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/20240730161350.png" style="zoom:50%">

| PS  | Input | NS  | Output |
| --- | ----- | --- | ------ |
| 00  | 0     | 00  | 0      |
| 00  | 1     | 01  | 0      |
| 01  | 0     | 00  | 0      |
| 01  | 1     | 10  | 0      |
| 10  | 0     | 00  | 0      |
| 10  | 1     | 00  | 1      |
