# <span id="ys">导航</span>
 [3](#3)  [4](#4)  [5](#5)  [6](#6 ) [7](#7) [18](#18) [19](#19) [21](#21)  [22](#22)  [23](#23) [24](#24)  [25](#25)  [26](#26)  [27](#27)  [28](#28)  [29](#29)  [35](#35)  [36](#36)  
## <span id="3">3</span>
```C++
可能不同，也可能不同。依编译器而决定。
```
## <span id="4">4</span> 
```C++
指令空间，数据空间，环境栈空间，形参变量，临时数据空间。
```
## <span id="5">5</span>
```C++
1) 3 * 8 = 24 bytes
2) 10 * 100 * 4 = 4000 bytes
3) 100 * 5 * 20 * 8 = 80,000 bytes
4) 10 * 10 * 10 * 5 * 4 = 20,000 bytes
5) 2 * 3 * 4 * 1 = 24 bytes
6) 3 * 3 * 3 * 3 * 4 = 324 bytes
```
## <span id="6">6</span> 
```C++

```
## <span id="7">7</span>
```C++
int factorial(int n)
{// Return n!.
   if (n <= 1)
      return 1;
   int fact = 2;
   for (int i = 3; i <= n; i++)
      fact *= i;
   return fact;
}
非递归版本: 0
递归版本:8 * max{n, 1}
总结:非递归版本使用的空间少于递归版本。
```
## <span id="18">18</span> 
```C++
2次
```
## <span id="19">19</span>
```C++
n - 1次, n > 1
0次 ， n<=1
```
## <span id="21">21</span>
```C++
numberOfRows * numberOfColumns
```
## <span id="22">22</span>
```C++
n(n-1)/2
```
## <span id="23">23</span>
```C++
n*n*n
```
## <span id="24">24</span>
```C++
m*p*n
```
## <span id="25">25</span>
```C++
设s(k,n)为perm(a, k,n)调用时的交换次数， 当k = n时s(k,n) = 0 ;  当 k < n时(n - k + 1)(2 + s(k+1, n));
通过重复替换，得到
s(1,n) = 2n + 2n(n - 1) + 2n(n - 1)(n - 2) + ... + 2n(n - 1)(n - 2) ... 2
= 2n! [sum from (i=1) to (n-1) (1 / (i!))]
```
## <span id="26">26</span>
```C++
2-24：
最好:n<0,t=0
最坏:n>1,t=3n
2-25：
最好:n<0,t=0
最坏:n>1,t=2n
```
## <span id="27">27</span>
```C++
n<1,t=0
n>1,t=n
```
## <span id="28">28</span>
```C++
最坏:n次
2-26快
```
## <span id="29">29</span>
```C++
1)
int stepCount;
void d(int x[], int n)
{
	for (int i = 0; i < n; i += 2)
	{
		++stepCount; //比较
		x[i] += 2;
		++stepCount;//+=
	}
	++stepCount;//for的最后一次比较

	int i = 1;
	++stepCount;//赋值

	while (i <= n / 2)
	{
		++stepCount;//比较
		++stepCount;//+=
		x[i] += x[i + 2];
		i++;
		++stepCount;//++
	}
	++stepCount;//while的最后一次比较
}
2)
int stepCount;
void d(int x[], int n)
{
	for (int i = 0; i < n; i += 2)
		stepCount += 2;

	stepCount += 2;
	int i = 1;
	while (i <= n / 2)
	{
		stepCount += 3;
		++i;
	}
	++stepCount;//while的最后一次比较
}
3)
for:2ceil(n/2)
while:3floor(n/2)
3 + 2ceil(n/2) + 3floor(n/2)
4)
______________________________________________________________________________
Statement                                s/e       Frequency      Total Steps
______________________________________________________________________________
void d(int x[], int n)                    0                0                0
{                                         0                0                0
   for (int i = 0; i < n; i += 2)         1    ceil(n/2) + 1    ceil(n/2) + 1
      x[i] += 2;                          1        ceil(n/2)        ceil(n/2)
   int i = 1;                             1                1                1
   while (i <= n/2)                       1   floor(n/2) + 1   floor(n/2) + 1
   {                                      0                0                0
      x[i] += x[i+1];                     1       floor(n/2)       floor(n/2)
      i++;                                1       floor(n/2)       floor(n/2)
   }                                      0                0                0
}                                         0                0                0
______________________________________________________________________________
Total                                            2ceil(n/2) + 3floor(n/2) + 3
______________________________________________________________________________
```
## <span id="35">35</span>
```C++
不，一个程序可以在一个输入上显示它的最坏时间行为，在另一个输入上显示它的最坏空间行为。
例如，我们可能有两种方法来解决同一个问题。一个可能很快，但会占用很多空间，而另一个可能很慢，但空间效率高。
我们可以将这两种方法合并到一个程序中，其中根据某些输入属性选择实际使用的解决方案方法。
满足这个特性的输入使用最坏情况空间运行得很快;不满足此属性的输入在最坏情况下运行，但使用最小的空间。
```
## <span id="36">36</span>
```C++
1)
t(n)=2(n+1)
2)
t(n)=(n+1)/2
3)
t(n)=n(n+1)
4)
t(n)=2^n
5)
t(n)=3^n
```
[回到导航](#ys)