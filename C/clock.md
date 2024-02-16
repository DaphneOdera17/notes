# clock

常数 $CLK\_TCK$ 是机器时钟每秒所走的时钟打点数

```c
#include<stdio.h>
#include<time.h>

clock_t start, stop;

double duration; // 单位 s

int main()
{
	start = clock(); // 开始计时
    MyFunction(); // 被测函数
    stop = clock(); // 停止计时
    duration = ((double)(stop - start)) / CLK_TCK;
    
    return 0;
}
```

