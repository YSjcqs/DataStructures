# <span id="ys">空降</span>

[1](#1)  [2](#2)  [3](#3)  [4](#4)  [5](#5)  [6](#6 ) [7](#7) [8](#8)  [9](#9)  [10](#10)  [11](#11)  [12](#12)  [13](#13) [14](#14)  [15](#15)  [16](#16)  [17](#17)  [18](#18) [19](#19)  [10](#20)  [21](#21)  [22](#22)  [23](#23) [24](#24)  [25](#25)  [26](#26)  [27](#27)  [28](#28)  [29](#29)  [30](#30)  [31](#30)  [32](#30)  [33](#33)  [34](#34)  [35](#35)  [36](#36)  [37](#37)  [38](#38)  [39](#39)  [40](#40)  [41](#41)  [42](#42)  [43](#43)  [44](#44)  [45](#45)  [46](#46)  [47](#47)  [48](#48) 

## <span id="1">1</span>

```C++
void swap(int& x,int& y)  
{//交换x和y
	int temp = x;  
	x=y;  
 	y =temp;  
}
```

## <span id="2">2</span> 

```C++
#include <iostream>

template<typename T,int n>
int count(const T(&a)[n], const T& value)
{
	int sum = 0;
	for (int i = 0; i != n; ++i)
		if (a[i] == value)
			++sum;
	return sum;
}
int main()
{
	int a[] = { 1,1,1,1,2,3,4,5,6,7 };
	std::cout << count(a, 1) << std::endl;
	return 0;
}
```

## <span id="3">3</span>

```C++
#include <iostream>

template<typename T,int n>
void fill(T(&a)[n], const T& value)
{
	int start = 0;
	int end = n;
	for (; start != end; ++start)
		a[start] = value;
}

int main()
{
	int arr[]{ 1,2,3,4,5 };
	fill(arr, 0);
	for (auto i : arr)
		std::cout << i << std::endl;
	return 0;
}
```

## <span id="4">4</span> 

```C++
#include <iostream>

template<typename T,int n>
T inner_product(const T(&a)[n],const T(&b)[n])
{
	T sum = 0;
	for (int i = 0; i != n; ++i)
		sum += a[i] * b[i];
	return sum;
}

int main()
{
	using namespace std;
	int a[] = { 1,2,3 };
	int b[] = { 1,2,3 };
	cout << inner_product(a, b) << endl;
	return 0;
}
```

## <span id="5">5</span>

```C++
#include <iostream>

template<typename T,int n>
void iota(T(&a)[n],const T& value)
{
	for (int i = 0; i != n; ++i)
		a[i] = value + i;
}

int main()
{
	using namespace std;
	int a[] = { 1,2,3 };
	iota(a, 4);
	for (auto i : a)
		cout << i << endl;
	return 0;
}
```

## <span id="6">6</span> 

```C++
#include <iostream>

template<typename T, int n>
bool is_sorted(const T(&a)[n])
{
	int i = 0;
	if (a[i] < a[i + 1])
	{
		for (i = 1; i != n - 1; ++i)
			if (a[i] < a[i + 1])
				continue;
			else
				return false;
	}
	else
	{
		for (i = 1; i != n - 1; ++i)
			if (a[i] > a[i + 1])
				continue;
			else
				return false;
	}
	return true;
}

int main()
{
	using namespace std;
	int a[] = { 1,2,3 };
	int b[]{ 3,2,1 };
	int c[]{ 2,1,3 };
	cout << is_sorted(a) << endl;
	cout << is_sorted(b) << endl;
	cout << is_sorted(c) << endl;
	return 0;
}
```

## <span id="7">7</span>

```C++
#include <iostream>

template<typename T, int n>
int mismatch(const T(&a)[n], const T(&b)[n])
{
	for (int i = 0; i != n; ++i)
		if (a[i] != b[i])
			return i;
	return -1;
}

int main()
{
	using namespace std;
	int a[] = { 1,2,3 };
	int b[]{ 3,2,1 };
	int c[]{ 1,2,4 };
	cout << mismatch(a, b)<< endl;
	cout << mismatch(a, c)<< endl;
	
	return 0;
}
```

## <span id="8">8</span> 

```C++
不同函数签名只由参数类型决定，它们的签名都是（int，int，int），
所以不具有不同签名。
```

## <span id="9">9</span>

```C++
(1)、调用int abc();
(2)、调用float abc();
(3)、报错：由于类型转换从两个float到 int和 int到 float是可能的。
(4)、报错：这里的参数类型为(double,double,double)，调用不明。
	再则，double到int和float有可能编译出错。
```

## <span id="10">10</span>

```C++
#include <iostream>

int abc(int a,int b,int c)
{
    if(a<0||b<0||c<0)
        throw 1;
    else if(a==0&&b==0&&c==0)
        throw 2;
    return a+b+c;
}

int main()
{
    try
    {
        //std::cout<<abc(2,-1,4)<<std::endl;
        std::cout<<abc(0,0,0)<<std::endl;
    }
    catch(int i)
    {
        std::cout<<i<<std::endl;
        return 1;
    }
    return 0;
}
```

## <span id="11">11</span>

```C++
#include <iostream>

template<typename T,int n>
int count(const T(&a)[n], const T& value)
{
    if(n<1)
        throw "n must be >=1";
	int sum = 0;
	for (int i = 0; i != n; ++i)
		if (a[i] == value)
			++sum;
	return sum;
}
int main()
{
	int a[] = { 1,1,1,1,2,3,4,5,6,7 };
    try
    {
	    std::cout << count(a, 1) << std::endl;
    }
    catch(char*  c)
    {
        std::cout<<c<<std::endl;
        return 1;
    }
	return 0;
}
```

## <span id="12">12</span>

```C++
#include <iostream>

template<typename T>
void make2Array(T**& arr, int numberOfRows, int* rowSize)
{
	arr = new T * [numberOfRows];
	for (int i = 0; i < numberOfRows; ++i)
	{
		arr[i] = new T[rowSize[i]];
		for (int j = 0; j < rowSize[i]; ++j)
			arr[i][j] = rowSize[i];
	}
}

int main()
{
	int** a;
	int rowSize[5]{ 1,2,3,4,5 };
	make2Array(a, 5, rowSize);
	for (int i = 0; i < 5; ++i)
		for (int j = 0; j < rowSize[i]; ++j)
			std::cout << a[i][j] << std::endl;

	return 0;
}
```

## <span id="13">13</span>

```C++
#include <iostream>
#include <algorithm>

template<typename T>
void changeLength1D(T*& arr, int oldLength, int newLength)
{
	if (newLength < 0)
		throw std::runtime_error("new length must be >=0");
	T* newArr = new T[newLength];
	int length = std::min(oldLength, newLength);
	std::cout << "length:" << length << std::endl;
	std::copy(arr, arr + length, newArr);
	delete[] arr;
	arr = newArr;
}

int main()
{
	int* arr = new int[3];
	for (int i = 0; i != 3; ++i)
		arr[i] = 0;
	changeLength1D(arr, 2, 6);
	for (int i = 0; i < 6; ++i)
		std::cout << arr[i] << std::endl;
	return 0;
}
```

## <span id="14">14</span>

```C++
#include <iostream>
#include <algorithm>

template<typename T>
void changeLength2D(T**& arr, int oldRow, int oldColumns,
	int newRow, int newColumns)
{
	if (newRow < 0 || newColumns < 0)
		throw std::runtime_error("new length must be >=0");

	T** newArr = new T * [newRow];
	for (int i = 0; i != newColumns; ++i)
		newArr[i] = new T[newColumns];
	int row = std::min(oldRow, newRow);
	int columns = std::min(oldColumns, newColumns);
	for (int i = 0; i != row; ++i)
		std::copy(arr[i], arr[i] + columns, newArr[i]);

	for (int i = 0; i != oldRow; ++i)
		delete[] arr[i];
	delete[] arr;
	arr = newArr;
}

int main()
{
	int** arr = new int* [3];
	for (int i = 0; i != 3; ++i)
		arr[i] = new int[3];

	for (int i = 0; i != 3; ++i)
		for (int j = 0; j != 3; ++j)
			arr[i][j] = j;
	changeLength2D(arr, 3, 2, 3, 4);
	for (int i = 0; i < 2; ++i)
		for (int j = 0; j < 4; ++j)
			std::cout << arr[i][j] << " ";
	std::cout << std::endl;
	return 0;
}
```

## <span id="15">15</span>

```C++
1)最大值：2^32-1 dollars and 99 cents  最小值：-max
2)最大值：2^31-1 dollars and 99 cents  最小值：-max
3)不超过：MAX_VALUE/100
```

## <span id="16">16</span> 

```C++
//1)
void input()
{
	cout << "Enter the currency amount with its sign dollars and cents" << endl;
	signType thesign;
	unsigned long thedollars;
	unsigned int thecents;
	cin >> thesign>>thedollars>>thecents;
	// set the value
	setValue(thesign,thedollars,thecents);
}

//2)   
currency subtract(const currency& x)
{
	currency result;
	long a1,a2,a3;
	a1=dollars*100+cents;
	if(sign==minus) a1=-a1;
	a2=x.dollars*100+x.cents;
	if(x.sign==minus) a2=-a2;
	a3=a1-a2;
	if(a3<0){result.sign=minus;a3=-a3;}
	else result.sign=plus;
	result.dollars=a3/100;
	result.cents=a3-result.dollars*100;
	return result;
}

// 3)  
currency percent(double x)
{
	currency result;
	long a1,a2;
	a1=dollars*100+cents;
	a2=(long)(a1*x/100);
	result.sign=sign;
	result.dollars=a2/100;
	result.cents=a2-result.dollars*100;
	return result;
}

// 4)  
currency multiply(double x)
{
	currency result;
	long a1,a2;
	a1=dollars*100+cents;
	a2=a1*x;
	result.sign=sign;
	result.dollars=(long)a2/100;
	result.cents=a2-result.dollars*100;
	return result;
}

//5)  
currency divide(double x)
{
	currency result;
	long a1,a2;
	a1=dollars*100+cents;
	a2=a1/x;
	result.sign=sign;
	result.dollars=(long)a2/100;
	result.cents=a2-result.dollars*100;
	return result;
}
```

## <span id="17">17</span>

```C++
void input()
{
	cout << "Enter the currency amount as a real number" << endl;
	double theValue;
	cin >> theValue;
	setValue(theValue);
}
   
currency subtract(const currency& x)
{
	currency result;
	result.amount = amount - x.amount;
	return result;
}
   
currency percent(float x)
{
	currency result;
	result.amount = (long) (amount * x / 100);
	return result;
}
   
currency multiply(float x)
{
	currency result;
	result.amount = (long) (amount * x);
	return result;
}
   
currency divide(float x)
{
	currency result;
	result.amount = (long) (amount / x);
	return result;
}
```

## <span id="18">18</span> 

```C++
此时你最不想看见的字是什么？没错，略！
```

## <span id="19">19</span>

```C++
#include <iostream>

int factorial(int n)
{
	if (n <= 1)
		return 1;
	int fact = 2;
	for (int i = 3; i <= n; ++i)
		fact *= i;
	return fact;
}

int main()
{
	std::cout << factorial(5) << std::endl;
	return 0;
}
```

## <span id="20">20</span>

```C++
//1)
#include <iostream>

int fibonacci(int n)
{
	if (n == 0)
		return 0;
	else if (n == 1)
		return 1;
	else
		return fibonacci(n - 1) + fibonacci(n - 2);
}

int main()
{
	std::cout << fibonacci(5) << std::endl;
	return 0;
}
//3)
#include <iostream>

int fibonacci(int n)
{
	if (n == 0)
		return 0;
	else if (n == 1)
		return 1;
	else
	{
		int fib = 0;
		int f0 = 0, f1 = 1;
		for (int i = 2; i <= n; ++i)
		{
			fib = f0 + f1;
			f0 = f1;
			f1 = fib;
		}
		return fib;
	}
}

int main()
{
	std::cout << fibonacci(5) << std::endl;
	return 0;
}

```

## <span id="21">21</span>

```C++
//3)
#include <iostream>

int fun(int n)
{
	return (n & 1) ? fun(3 * n + 1) : n / 2;
}

int main()
{
	std::cout << fun(5) << std::endl;
	return 0;
}
//4)
#include <iostream>

int fun(int n)
{
	return (n & 1) ? (3 * n + 1) / 2 : n / 2;
}

int main()
{
	std::cout << fun(7) << std::endl;
	return 0;
}
```

## <span id="22">22</span>

```C++
#include <iostream>
#include <algorithm>

int A(int i, int j)
{
	if (i == 1 && j >= 1)
		return std::pow(2, j);
	else if (i >= 2 && j == 1)
		return A(i - 1, 2);
	else
		return A(i - 1, A(i, j - 1));
}

int main()
{
	std::cout << A(2, 2) << std::endl;
	return 0;
}
```

## <span id="23">23</span>

```C++
#include <iostream>

int gcd(int x, int y)
{
	if (x == 0)
		return y;
	else if (y == 0)
		return x;
	else
		return gcd(y, x % y);
}
int main()
{
	std::cout << gcd(20, 30) << std::endl;
	return 0;
}
```

## <span id="24">24</span>

```C++
#include <iostream>

template<typename T,int n>
bool fun(const T(&a)[n], T x, int pos)
{
	if (pos >= n)
		pos = n - 1;
	if (pos == -1)return false;
	else if (a[pos] == x)return true;
	else return fun(a, x, pos - 1);
}

int main()
{
	int a[]{ 1,2,3,4,5 };
	int x = 1;
	std::cout << fun(a, x, 6) << std::endl;
	return 0;
}
```

## <span id="25">25</span>

```C++
#include <iostream>
template<typename T>
void sg(T* a, int* mark, int b, int l)
{//a为集合元素，mark为标记数组，b为起点，l为元素个数
	if (b == l)
	{
		std::cout << "{ ";
		for (int i = 0; i < l; i++)
		{
			std::cout << mark[i];
			/*if (mark[k] == 1)
				std::cout << a[k];*/
		}
		std::cout << "}" << std::endl;
		return;
	}

	mark[b] = 0;
	sg(a, mark, b + 1, l);
	mark[b] = 1;
	sg(a, mark, b + 1, l);
}
int main()
{
	int mark[3]{ 0,0,0 };
	char a[3] = { 'a','b','c' };
	sg(a, mark, 0, 3);
	return 0;
}
```

## <span id="26">26</span>

```C++
#include <iostream>
void gc(int n)
{
    if (n <= 0)
        throw std::runtime_error("n >=0");
    if (n == 1)
        std::cout << 1 << ",";
    else
    {
        gc(n - 1);
        std::cout << n << ",";
        gc(n - 1);
    }
}
int main()
{
    gc(3);
    std::cout << std::endl;
    return 0;
}
```

## <span id="27">27</span>

```C++
#include <iostream>

template<typename InputIt, typename T>
T accumulate(InputIt first, InputIt last, T init)
{
	for (; first != last; ++first)
		init += *first;
	return init;
}

int main()
{
	int arr[]{ 1,2,3,4,5 };
	std::cout << accumulate(arr,arr+5,0) << std::endl;
	return 0;
}
```

## <span id="28">28</span>

```C++
#include <iostream>
#include <algorithm>

template<typename InputIt, typename T, 
	typename BinaryOperation>
T accumulate(InputIt first, InputIt last, 
	T init, BinaryOperation op)
{
	for (; first != last; ++first)
		init = op(init, *first);
	return init;
}

int main()
{
	int arr[]{ 1,2,3,4,5 };
	std::cout << accumulate(arr,arr+5,1,std::multiplies<int>()) << std::endl;
	return 0;
}
```

## <span id="29">29</span>

```C++
#include <iostream>
#include <vector>

template<typename InputIt,typename OutputIt>
OutputIt myCopy(InputIt first, InputIt last, 
	OutputIt to_first)
{
	for (; first != last; ++first)
		*to_first = *first++;
}

int main()
{
	std::vector<int> vi1{1, 2, 3};
	std::vector<int> vi2(4, 0);
	copy(vi1.begin(), vi1.end(), vi2.begin());
	for (auto e : vi2)
		std::cout << e << std::endl;
	return 0;
}
```

## <span id="30">30</span>

```C++
#include <iostream>
#include <iterator>
#include <algorithm>
using namespace std;
template<typename T>
void permutations1(T list[], int k, int m)
{//程序1-32，递归函数生成排列
	if (k == m - 1)
	{
		copy(list, list + m, ostream_iterator<T>(cout, "  "));
		cout << endl;
	}
	else
		for (int i = k; i <= m - 1; i++)
		{
			swap(list[k], list[i]);
			permutations1(list, k + 1, m);
			swap(list[k], list[i]);
		}
}
template<typename T>
void permutations2(T list[], int k, int m)
{//练习30
	sort(list, list + m);
	do {
		copy(list, list + m, ostream_iterator<T>(cout, " "));
		cout << endl;
	} while (next_permutation(list, list + m));
}
template<typename T>
void permutations3(T list[], int k, int m)
{//练习31		
	T temp[3];
	copy(list, list + m, temp);
	do {
		copy(list, list + m, ostream_iterator<T>(cout, " "));
		cout << endl;
	} while (next_permutation(list, list + m));
	while (prev_permutation(temp, temp + m))
	{
		copy(temp, temp + m, ostream_iterator<T>(cout, " "));
		cout << endl;
	}
}
template<typename T>
void permutations4(T list[], int k, int m)
{//练习32
	while (next_permutation(list, list + m)) {}
	do {
		copy(list, list + m, ostream_iterator<T>(cout, " "));
		cout << endl;
	} while (next_permutation(list, list + m));
}
int main()
{

	char ch[]{ 'c','b','a' };
	permutations1(ch, 0, 3);
	cout << "-----------" << endl;
	permutations2(ch, 0, 3);
	cout << "-----------" << endl;
	char ch3[]{ 'c','a','b' };
	permutations3(ch3, 0, 3);
	cout << "-----------" << endl;
	char ch4[]{ 'c','a','b' };
	permutations4(ch4, 0, 3);
	return 0;
}
```

## <span id="33">33</span>

```C++
#include <iostream>

int main()
{
	int arr[]{ 1,1,1,1,2,3,4 };
	std::cout<<std::count(arr, arr + 7, 1) << std::endl;
	return 0;
}
```

## <span id="34">34</span>

```C++
#include <iostream>

int main()
{
	int arr[4]{ 0 };
	std::fill(arr, arr + 4, 1);
	for (auto e : arr)
		std::cout << e << " ";
	std::cout << std::endl;
	return 0;
}
```

## <span id="35">35</span>

```C++
#include <iostream>
#include <numeric>

int main()
{
	int a[]{ 1,2,3 };
	int b[]{ 1,2,3,4 };
	std::cout << std::inner_product(a, a + 3, b, 0) << std::endl;
	return 0;
}

```

## <span id="36">36</span>

```C++
#include <iostream>
#include <numeric>

int main()
{
	int arr[5]{ 0 };
	std::iota(arr, arr + 5, 1);
	for (auto e : arr)
		std::cout << e << std::endl;
	return 0;
}
```

## <span id="37">37</span>

```C++
#include <iostream>
#include <algorithm>

int main()
{
	using namespace std;
	int a[]{ 1,3,2,4,5 };
	int b[]{ 1,2,3 };
	int c[]{ 3,2,1 };
	if (is_sorted(c, c + 3))
		cout << "YES" << endl;
	else
		cout << "NO" << endl;
	return 0;
}
```

## <span id="38">38</span>

```C++
#include <iostream>
#include <algorithm>

int main()
{
	using namespace std;
	int a[]{ 1,2,3,4 };
	int b[]{ 1,2,4,3 };
	cout << *(mismatch(a, a + 4, b).first) << endl;
	cout << *(mismatch(a, a + 4, b).second) << endl;
	return 0;
}
```

## <span id="39">39</span>

```C++
#include <iostream>

template<typename InputIt, typename T>
int count(InputIt first, InputIt last, T value)
{
	int sum = 0;
	for (; first != last; ++first)
		if (*first == value)
			sum += 1;
	return sum;
}

int main()
{
	int arr[]{ 1,1,1,1,2,3,4 };
	std::cout << count(arr, arr + 7, 1) << std::endl;
	return 0;
}
```

## <span id="40">40</span>

```C++
#include <iostream>

template<typename InputIt,typename T>
void fill(InputIt first, InputIt last, T value)
{
	for (; first != last; ++first)
		*first = value;
}

int main()
{
	int arr[4]{ 0 };
	fill(arr, arr + 4, 1);
	for (auto e : arr)
		std::cout << e << " ";
	std::cout << std::endl;
	return 0;
}

```

## <span id="41">41</span>

```C++
#include <iostream>

template<typename InputItL,typename InputItR,
	typename T>
	T inner_product(InputItL firstL, InputItL lastL,
		InputItR firstR, T init)
{
	for (; firstL != lastL; ++firstL, ++firstR)
		init += (*firstL * *firstR);
	return init;
}

int main()
{
	int a[]{ 1,2,3 };
	int b[]{ 1,2,3,4 };
	std::cout << inner_product(a, a + 3, b, 0) << std::endl;
	return 0;
}
```

## <span id="42">42</span>

```C++
#include <iostream>

template <typename ForwardIt, typename T>
void iota(ForwardIt first, ForwardIt last, T val)
{
	for (; first != last; ++first, ++val)
		*first = val;
}

int main()
{
	int arr[5]{ 6 };
	iota(arr, arr + 5, 1);
	for (auto e : arr)
		std::cout << e << std::endl;
	return 0;
}
```

## <span id="43">43</span>

```C++
#include <iostream>

template<typename ForwardIt>
bool is_sorted(ForwardIt first, ForwardIt last)
{
	if (first == last)
		return true;
	for (ForwardIt next = first; ++next != last;++first)
		if (*next < *first)
			return false;
	return true;
}

int main()
{
	int a[]{ 1,2,3,4,5 };
	int b[]{ 5,4,3,2,1 };
	std::cout << is_sorted(a, a + 5) << std::endl;
	std::cout << is_sorted(b, b + 5) << std::endl;
	return 0;
}
```

## <span id="44">44</span>

```C++
#include <iostream>

template<typename InputItL,typename InputItR>
std::pair<InputItL,InputItR>
mismatch(InputItL firstL, InputItL lastL, InputItR firstR)
{
	while ((firstL != lastL) && (*firstL == *firstR))
		++firstL, ++firstR;
	return std::make_pair(firstL, firstR);
}

int main()
{
	using namespace std;
	int a[]{ 1,2,3,4 };
	int b[]{ 1,2,4,3 };
	cout << *(mismatch(a, a + 4, b).first) << endl;
	cout << *(mismatch(a, a + 4, b).second) << endl;
	return 0;
}

```

## <span id="45">45</span>

```C++
void outputRoots(const double& a, const double& b, const double& c)
{//计算和输出二次方程的根
	double d = b * b - 4 * a * c;	①	
	if(d>0) {//两个实数根}		②
	else if(d==0) {//两个根相同}	③
	else {//复数共轭根}		④
}

语句覆盖:1+2，1+3，1+4
分支覆盖:d<0,d+0,d>0
从句覆盖:d<0,d+0,d>0
执行路径覆盖:1+2，1+3，1+4
```

## <span id="46">46</span>

```C++
int a[]{ 1,2,3 };
测试集：(a,3)
```

## <span id="47">47</span>

```C++
template<typename T>
T sum(T a[], int n)
{
	T theSum = 0;				①
	for (int i = 0; i < n; i++)		②
		theSum += a[i];			③
	return theSum;				④
}

n<0:1,2,4
n=0:1,2,4
n=1:1,2,3,2,4
n=2:1,2,3,2,3,2,4
不能提供分支覆盖：只有一条执行路径
```

## <span id="48">48</span> 

```C++
template<typename T>
T rSum(T a[], int n)
{
	if(n>0)					①
		return rSum(a,n-1)+a[n-1];	②			
	return theSum;				③		
}

n<0:1,3
n=0:1,3
n=1:1,2,1,3
n=2:1,2,1,2,1,3
不能提供分支覆盖：只有一条执行路径
```

[回到导航](#ys)