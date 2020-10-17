## 编译方式

```
% gcc -o 输出文件名 代码.c
```

## 指令

```c
#include <stdio.h>
```

指令以<u>#</u>开头，默认<u>只占一行</u>，结尾<u>没有</u>分号等标记

## 声明变量

声明必须放在语句前（但是在C99之后允许不在语句前），且声明和语句间最好留出一个空行

类型+名字1,名字2...

```c
int height, length;
float profit, loss;
```

## 宏定义

```c
#define INCHES_PER_POUND 166 /*宏的名字最好只用大写字母*/
#define RECIPROCAL_OF_PI (1.0f / 3.14159f) /*表达式必须用括号括起来*/
```

## printf()

```c
printf("balabala %d %f %lf", integer, float_value, double_value);
//================整数================
// %u 无符号十进制整数
// %o 无符号八进制整数
// %x 无符号十六进制整数
// %hd 短整数
// %ld 长整数
// %lld 长长整数（C99中）
//================浮点数==============
// %e 科学计数法的浮点数
// %f float类型
// %g 可以表示e和f，但小数末尾的0不会显示
// %lf double类型（只能在scanf中使用），也可以是le,lg
// %Lf long double类型（这个printf也可以用）
//================其他=================
// %c char类型
// %zu sizeof(int)类型（在C99中可以使用）
```

#### 转换说明符

通用格式：%-m.pX

- -：有是左对齐，没有是右对齐
- m: 字符的个数
- X：看上面的代码注释
- p：d时为数字的个数（不够要在前面加0），e和f时为小数点后数字的个数，g时为有效数字

#### 转义序列

- 字符转义序列见书中P97
- 数字转义序列见书中附录E，使用时八进制用"\"，十六进制用"\x"（x小写），且要用单引号括起来，通常可以考虑使用宏来定义一个新的命名

## scanf()

```c
scanf("%d", &integer);
scanf("%f", &float_value);
scanf("%lf", &double_value);
scanf("%1d", &YiWeiZhengShu);
```

## if-else语句

```c
if(表达式){
    语句1;//只有一条的时候可以省略大括号
    语句2;
    ...;
}
else if(表达式){
    语句1;//只有一条的时候可以省略大括号
    语句2;
    ...;
}
else(表达式){
    语句1;//只有一条的时候可以省略大括号
    语句2;
    ...;
}
```

上面的等价于：

```c
if(表达式){
    语句1;//只有一条的时候可以省略大括号
    语句2;
    ...;
}
else {
    if(表达式){
        语句1;//只有一条的时候可以省略大括号
        语句2;
        ...;  
    }
    else(表达式){
        语句1;//只有一条的时候可以省略大括号
        语句2;
        ...;
    }
}

```

## 条件表达式

```c
表达式1 ? 表达式2 : 表达式3;
```

如果1成立那么2，反之3。每个表达式都是<u>**求值**</u>用的。

例子：

```c
i = 1;
j = 2;
k = i > j ? i : j;//因为i > j为否（0），因此k = j
```

## 布尔变量

在c语言中并没有布尔类型的变量。在C99中，一个新的头文件提供了相关的布尔宏。例子：

```c
#include<stdbool.h>
bool flag;
flag = false;
flag = true;
```

## switch语句

```c
switch (grade){//可以用整数和字符，但不可以用浮点数和字符串
    //case后面的常量表达式不能包含变量和函数调用，且只能有一个
    //但是多个case可以放置在同一组语句的前面
    case 5:
    case 4:  printf("A");
        	 break;
    case 3:  printf("B");
        	 break;
  //case 2:......
    //default可以没有    
    default: printf("Illegal grade");
             break;
}
```

## while语句

```c
while(表达式){
    语句;
}
```

## do语句

```c
do{
    语句;
}while(表达式);
```

do语句的好处在于至少可以执行一次

## for语句

```c
for(表达式1;表达式2;表达式3){
    语句;
}
```

在C99中，允许在表达式1处声明变量，该变量只可以在循环内访问。

## 退出循环语句

```c
break;//只能跳出一层嵌套
continue;//只用于循环，且不跳出循环
goto 标识符;//很少使用
标识符:
//标识符内容
```

## 基本类型

#### 整数类型

```c
(unsigned) short int, int,long int//unsigned表示无符号位，int可省略（推荐省略）,数字以U，L或UL结尾
long long int//C99中新添加的，以LL结尾
```

整数类型的取值范围与CPU位数和编译器有关

#### 浮点类型

```c
float, double, long double
```

#### 字符类型

```c
char ch = 'a';
```

在c中，字符实际上被当成小整数来处理

##### 字符处理函数

```c
#include <ctype.h>
ch = toupper(ch); //小写转大写
ch = getchar();//读取字符，返回的实际是一个int型
putchar(ch);//类似于printf
//getchar在搜索字符的循环和跳过字符的循环中的应用
while((ch = getchar()) == ' '){
    ;
}
//循环终止时，变量ch将包含getchar函数遇到的第一个非空白字符
```

#### 类型转换

在赋值过程中，等号右边的表达式会被转换成左边变量的类型

强制类型转换格式：（类型名） 表达式

```c
float a, b;
b = a - (int)b;
```

#### 类型定义

```c
typedef float Dollars;
Dollars cash_in;
```

#### sizeof运算符

```c
sizeof(类型名或变量名);//值为无符号整数，类型为size_t，代表存储类型名的值所需的字节数
```

