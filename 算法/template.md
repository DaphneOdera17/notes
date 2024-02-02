

```c++
template<typename T>
void selectionSort(T arr[], int n)
{
	for(int i = 0; i < n; i ++)
    {
		int minIndex = i;
        for(int j = i + 1; j < n; j ++)
         	if(a[minIndex] > a[j])
                minIndex = j;
       
        swap(arr[i], arr[minIndex]);
    }
}
```

使用 $template$ 可以让它泛化成为一个模板函数，不管 $a$ 数组是 $int$ 类型还是 $float$ 类型，都可以进行选择排序



 