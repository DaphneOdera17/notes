# $FILE$

$FILE$ 类型指针可以创建、打开、读取和写入文件，并且使用 $fopen()$ 函数

```c
FILE *fptr;
fptr = fopen(filename, mode);
```

##### **$mode$**	

1. $\textcolor{red}w - Writes~to~a~file$
2. $\textcolor{red}a-Appends~new~data~to~a~file$
3. $\textcolor{red}r-Reads~from~a~file$



```c
FILE *fptr;

//Create a file
// w 模式用于写入文件，但是如果该文件不存在，会为我们创建一个
//未指定路径的话，默认创建路径与 c 文件相同
fptr = fopen("filename.txt", "w");

//Close the file
fclose(fptr);
//make sure that changes are saved properly
//other programs can use the file
//clean up unnecessary memory space
```

可以提供相对路径

```c
fptr = fopen("C:\directoryname\filename.txt", "w");
```

用 $fprintf()$ 可以写入

```c
FILE *fptr;

fptr = fopen("filename.txt", "w");
fprintf(fptr, "Some text");
fclose(fptr);
```

但是如果用它来写入的话，如果写入已经存在的文件，旧内容将被删除，并插入新内容。

用 $a$ 模式可以只添加新内容而不删除就得内容

如果 $a$ 模式写入的文件夹不存在，那么它将创建一个带有附加内容的新文件



读取文件可以使用 $r$ 模式

```c
FILE *fptr;

// Open a file in read mode
fptr = fopen("filename.txt", "r");
```

然后创建一个足够大的字符串来存储文件的内容

```c
char myString[100];
```

可以使用 $fgets()$ 函数来读取文件的内容

```c
fgets(myString, 100, fptr);
```

第一个参数指定存储文件内容的位置，第二个参数指定要读取的数据的最大大小，第三个参数需要一个用于读取文件的文件指针

但是 $fgets()$ 只能读取文件的第一行，所以如果要读取文件的每一行，可以使用 $while$ 循环

```c
while(fgets(myString, 100, fptr))
{
    printf("%s", myString);
}
```



当我们尝试打开不存在的文件进行读取，$fopen()$ 函数将会返回 $NULL$

```c
FILE *fptr;

// Open a file in read mode
fptr = fopen("loremipsum.txt", "r");

// Print some text if the file does not exist
if(fptr == NULL) {
  printf("Not able to open the file.");
}

// Close the file
fclose(fptr);
```

![image-20231211124037705](https://typora-birdy.oss-cn-guangzhou.aliyuncs.com/image-20231211124037705.png)