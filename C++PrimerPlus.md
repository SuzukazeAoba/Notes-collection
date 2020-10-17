# 预备知识

### 编译方法

```
g++ Hello.cpp
```

# 开始学习C++

### C++程序基本结构

```c++
#include <iostream>

int main(){
    using namespace std;
    
    cout << "Come up and C++ me some time.";
    cout << endl;
    cout << "You won't regret it!" << endl;
    
    return 0;
}
```

### `main`函数

```c++
int main(){
    statements;
    return 0;
}
```

### 添加注释

```c++
//这是一条注释
```

### 使用`cout`进行输出

```c++
cout << "I have " << carrots << " carrots" << endl;
```

`cout`是一个预定义的对象，知道如何显示字符串，数字和单个字符等。

### 使用`cin`进行输入

```c++
cin >> carrots;
```

### 创建函数

```c++
void function1();

int main(void){
  //...
}

void function1(void){
  //...
}
```

需要提供函数原型（prototype），即上述代码中第一行的信息。

# 处理数据

### 变量初始化

```c++
int owls = 101;
int wrens(432);
int hamburgers = {24}; //C++98
int emus{7}; //C++11
int rocs = {}; // rocs = 0
int psychics{};
```



### 整数类型

- `short`：至少16位
- `int`: 至少和short一样长
- `long`: 至少32位，且至少与int一样长
- `long long`: 至少64位，且至少与long一样长
- `unsigned`: 代表无符号整型

### 字符类型

- `char`
- `wchar_t`
- `char16_t` (C++11)
- `char32_t` (C++11)

字符本质上是用整数来表示的

### 布尔类型

真为`true`，假为`false`

### 浮点数

- `float`：只有6位有效数字
- `double`
- `long double`

### `const`限定符声明常量

```c++
const int MONTHS = 12;
```

### 算术运算符

`+ - * / %`

取余操作数只能是整数。所有运算符的优先级和结合性见附录D。

### 强制类型转换

`(long) thron`

`static_cast<long> (thorn)`

# 复合类型

### 数组

```c++
short a[3] = {1, 2, 3};
int b[3];
```

只有在定义数组时才可以使用初始化。数组不能被赋给另一个数组。初始化时如果提供的值少于数组的元素数目，则编译器讲把其他元素设置为0。

在C++11中，等号可以省略。如果大括号内不包含任何东西，所有元素都设置为0。

如果初始化时方括号内为空，则编译器将计算元素个数。如下述代码所示：

```c++
short things[] = {1, 5, 3, 6};
int num_elements = sizeof things / sizeof (short);
```

这种方法在初始字符串时比较安全。

### C风格字符串

#### 声明字符串

```c++
char fish[] = "Bubbles";
```

字符串结尾为一个空字符`'\0'`。

#### 拼接字符串常量

```c++
cout << "I'd give my right arm to be" " a great violinist.\n";
cout << "I'd give my right arm to be a great violinist.\n";
```

上述两个语句等效。拼接时不会在连接的字符串间添加空格。第一个字符串中的`'\0'`将被第二个字符串的第一个字符取代。

#### 标准头文件`cstring`

`cstring`提供了很多与字符串相关的函数声明，如`strlen()`等。

#### 面向行的输入

```c++
cin.getline(name, 20);
```

将姓名读入到一个包含20个元素的name数组中。最多读取19个字符，留下一个给空字符。它通过换行符来确定结尾，之后换行符会被空字符替代。

```c++
cin.get(name, ARSIZE);
cin.get();
cin.get(dessert, ARSIZE);
cin.get();

cin.get(name, ARSIZE).get();
```

`get()`由于不会舍弃最后的换行符，因此中间需要用一个`cin.get()`来跨过换行符。由于该函数返回一个cin对象，因此第一二行可以拼接起来使用变成最后一行。

`getline()`使用起来更简单一些，`get()`使得检查错误更简单一些。

#### 混合输入数字与字符串

由于`cin`读取一个数字变量后会把换行符留在输入队列中，这会使得下一次试图读取字符串时因为一个读取了换行符而将空字符串赋值给该字符串。因此应使用一个`cin.get()`来处理该换行符。如：

```c++
cin >> year;
cin.get();

(cin >> year).get();
```

上述两种方法等价。

### string类

#### 声明

string类需要包含头文件`string`，该类位于名称空间`std`中，因此使用时需要提供一条`using`指令。

```c++
string str1;
string str2 = "panther";
cin >> str1;
```

类设计使程序能够自动处理string的大小。上例中第一行声明了一个长度为0的string，而使用`cin`时`str1`的长度将被自动调整。

#### 一些常用的方法

```c++
string str1;
string str2 = "panther";
string str3;

str1 = str2; // 可赋值
str3 = str1 + str2; // 可使用+拼接字符串
str1 += str2; // 在str1结尾添加str2
int len1 = str1.size(); // 获取字符串长度
```

#### 读取行到string类中

```c++
getline(cin, str);
```

### 结构

```c++
//定义
struct inflatable{
  char name[20];
  float volume;
  double price;
};
//声明
inflatable guest = {
  "Gloria",
  1.88,
  29.99
};
cout << guest.name;
//声明结构数组
inflatable guests[2] = {
  {"Bambi", 0.5, 21.99},
  {"Godzilla", 2000, 565.99}
};

```

注意结尾要有一个分号。C++中声明结构变量时可以省略`struct`。

外部声明可以在后面的任何函数使用，而内部声明只能被其所属函数使用。

在C++11中，初始化时等号可以被省略。若大括号内为空，则所有成员都会被设置为0。

可以使用string类作为成员，只是需要让结构定义能够访问名称空间`std`。

### 共同体

```c++
//定义
union one4all{
  int intVal;
  long longVal;
  double doubleVal;
};
//声明及使用
one4all pail;
pail.intVal = 15;
cout << pail.intVal;
pail.doubleVal = 1.38;
cout << pail.doubleVal;
```

共用体只能同时存储其中一个成员的值。

### 枚举

```c++
enum spectrum{
  red, // red = 0
  orange = 0, //orange = 0
  yellow, // yellow = orange + 1 = 1
  green,
  blue,
  violet,
  indigo = 100,
  ultraviolet // ultraviolet = indigo + 1 = 101
};

spectrum band = blue;
band = spectrum(3);
```

### 指针

#### 声明指针

```c++
int updates = 6;
int* pUpdates;
pUpdates = &updates;
```

变量`updates`表示值，通过`&`运算符获取地址；变量`pUpdates`表示地址，通过`*`运算符获取值。

`*`两边的空格是可选的。C++程序员常用上述格式以强调`int*`是一种类型：指向`int`的指针。

对于每一个指针变量名都要使用一个`*`。

在C++中，值为`0`的指针被称为空指针(null pointer)。

#### 指针的危险

C++中创建指针时，计算机将分配用来存储地址的内存，但不会分配用来存储指针所指向的数据的内存。为数据提供空间是一个独立的步骤。忽略这一步很可能导致指针指向的地方不是要存储数据的地方。

因此，一定要在对指针应用`*`运算符之前，将指针初始化为一个确定的，适当的地址。

#### 使用`new`分配内存

```C++
int* pn = new int;
```

`new`从堆(heap)或自由存储区(free store)的内存区域分配内存，而变量都是存储在栈(stack)的内存区域中。

#### 使用`delete`释放内存

```c++
int* ps = new int;
//...
delete ps;
```

释放的是指针指向的内存，不会删除指针本身。

一定要配对使用`new`和`delete`，否则会发生内存泄漏。

不要尝试释放已经释放的内存块。

不能用`delete`来释放声明变量所获得的内存。

使用`delete`的关键在于，将它用于`new`分配的内存。这并不意味着要使用用于`new`的指针，而是用于`new`的地址。

#### 创建动态数组

```C++
int* psome = new int [10];
psome[2] = 1;
//...
delete [] psome;
```

数组名的值不可以改变，而指针的值可以改变。将指针的值+1后，其增加的值等于指向的类型占用的字节数。

对数组名运用`sizeof`运算符得到的是数组的长度，而对指针运用`sizeof`运算符得到的是指针的长度。

#### 数组的地址

数组名被解释为其第一个元素的地址。对数组名应用地址运算符时，得到的是整个数组的地址。

#### 创建动态结构

```c++
inflatable* ps = new inflatable; //创建结构
ps->price = ...; //访问成员
```

#### 模板类`vector`

```c++
#include <vector> //包含头文件
//...
using namespace std; //包含在std中
vector<int> vi; //创建一个size为0的int型array

int n;
cin >> n;
vector<double> vd(n); //创建一个n个double变量的array
```

#### 模板类`array`(C++11)

```c++
#include <array>
//...
using namespace std;
array<int, 5> ai; //size不能是变量
array<double, 4> ad = {1.2, 2.1, 3.43, 4.3};
```

#### 数组，`vector`，`array`的比较

- 三者都可以使用标准数组表示法来访问各个元素
- `array`和数组存储在相同的内存区域（栈）中，而`vector`存储在另一个区域（自由存储区或堆）中
- 可以将一个array对象赋值给另一个，而数组必须逐个复制数据
- 对于超界错误，数组无法禁止，而另外两个可以使用成员函数`at()`，但代价是花费时间更长

# 循环和关系表达式

### `for`循环

```c++
for (i = 0; i < 100; i++){
  cout << i;
  cout << endl;
}
```



### 递增`++`递减`--`运算符

简单来说，前缀为修改后使用，后缀为使用后修改

当前缀还是后缀对程序行为本身没有影响时，对于内置类型，采用哪种格式不会有差别，但对于用户定义的类型，则前缀的效率更高。

### 组合赋值运算符

`+= -= *= /= %=`

### 复合语句（代码块）

```c++
{
  //语句1
  //语句2
  //...
}
```

代码块由一对花括号和它们包含的语句组成，被视为一条语句。

如果在语句块中定义一个新的变量，则仅当程序执行该语句块中的语句时该变量才存在。执行完后该变量被释放。

在外部语句块中定义的变量在内部语句块中也是被定义了的。

如果在一个语句块中声明一个和外部某个变量同名称的变量，则在该语句块范围内将使用新变量，之后旧变量再次可见。

### 关系表达式

`< > <= >= == !=`

### 字符串比较

C风格字符串应使用`strcmp()`函数比较，若字符串相同则返回`0`，若第一个字符串按字母顺序排在第二个字符串之后，则返回一个正数值，反之返回一个负数值。但字符本身可以用关系表达式比较。

`string`类字符串则可以直接使用关系运算符，只要至少有一个操作数为`string`对象，即另一个操作数可以使C风格字符串。

### `while`循环

```c++
while(i != 0){
 //语句1...
 //语句2...
}
```

### `clock()`函数

```c++
#include <iostream>
#include <ctime>

int main(){
  using namespace std;
  
  cout << "Enter the delay time in seconds: ";
  float secs;
  cin >> secs;
  
  clock_t delay = secs * CLOCKS_PER_SEC;
  
  cout << "starting\a\n";
  clock_t start = clock();
  while(clock() - start < delay);
  
  cout << "done \a\n";
  
  return 0;
}
```

### 类型别名

```c++
#define BYTE char
typedef char byte;
```

使用`define`声明一系列变量时不适用，而`typedef`不会有这样的问题。

`typedef`不会创建新类型，只是为已有类型建立一个新的名称。

### `do while`循环

```c++
do{
  //...
}while();
```

### 基于范围的for循环（C++11）

```c++
double prices[5] = {4,99, 10.99, 6.87, 7.99, 8.49};
for (double x : prices){
  cout << x;
  cout << endl;
}
for (double &x : prices){
  x = x * 0.8;
}
for (int x : {1, 2, 3, 4, 5}){
  cout << x << " ";
}
cout << endl;
```

### 循环和文本输入

使用`cin`读取`char`值时将忽略空格和换行符。可以通过`cin.get(ch)`函数补救这一点（`ch`为变量名）。

### 文件尾条件

每次读取一个字符，直到遇到`EOF`的输入循环的基本设计：

```c++
cin.get(ch);
while(!cin.fail()){
  //...
  cin.get(ch);
}
//简化版本
while(cin.get(ch)){
  //...
}
```

