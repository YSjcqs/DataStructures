## 1
```C++
1)
[0][0][0][0] [0][0][0][1] [0][0][1][0] [0][0][1][1]


[0][1][0][0] [0][1][0][1] [0][1][1][0] [0][1][1][1]


[0][2][0][0] [0][2][0][1] [0][2][1][0] [0][2][1][1]


[1][0][0][0] [1][0][0][1] [1][0][1][0] [1][0][1][1]


[1][1][0][0] [1][1][0][1] [1][1][1][0] [1][1][1][1]


[1][2][0][0] [1][2][0][1] [1][2][1][0] [1][2][1][1]
 2)
map(i1, i2, i3, i4) = i1 *u2* u3* u4 + i2* u3 *u4 + i3 *u4 + i4
```
## 2
```C++
map(i1,i2,i3,i4,i5) = i1*u2*u3*u4*u5+i2*u3*u4*u5+i3*u4*u5+i5*u5+i5
```
## 3

```C++
map(i1, i2, ..., ik) = i1 u2 u3 ... uk + i2 u3 ... uk + ... + ik-2 uk-1 uk + ik-1 uk + ik
    
map(i1, i2, ..., ik) = map(i1, ... , ik-1) * uk + ik
```
##  5

```C++
2)
map(i1, i2, i3, i4) = i4 u3 u2 u1 + i3 u2 u1 + i2 u1 + i1
```
## 6

```C++
map(j1,j2,...jk)=
	(j1*u2*u3 ... uk）+（j2*u3 ... uk）+...+（jk-2*uk-1*uk）+（jk-1*uk）+（jk)
    
```



## 7

```C++
1)
[2][0] [2][1] [2][2] [2][3] [2][4] [1][0] [1][1] [1][2] [1][3] [1][4]
[0][0] [0][1] [0][2] [0][3] [0][4]
2）
map(i1, i2) = (u1 - i1 - 1)u2 + i2
```
## 9

```C++
1）
1 x 10 x 4 + 10 x 2 x 4 = 120 bytes
10 x 2 x 4 = 80 bytes
2）
(4mn + 4m) / (4mn) = 1 + 4/n
```
## 10

```C++
1）
20 X 4 + 4 X 4 + 10 X 4 X 2 X 4=416 bytes
2)
(4mnp+4m+4n)/(4mnp) 
```
## 13

```C++
1)
The transpose is
7 0 6 8 1
2 1 4 2 4
0 0 2 7 9
9 5 0 3 6

2)
The product is
134   47   50    87   69
 47   26    4    17   34
 50    4   56    70   40
 87   17   70   126   97
 69   34   40    97  134
```
## 15

```C++
template<class T>
std::ostream& operator<<(std::ostream& out, const matrix<T>& theMatrix)
{
	int k = 0;
	for (int i = 0; i < theMatrix.rows; ++i)
		for (int j = 0; j < theMatrix.columns; ++j)
			out << theMatrix.element[k++] << " ";
	out << std::endl;
	return  out;
}

template<class T>
matrix<T>& matrix<T>::operator+=(const T& x)
{
	for (int i = 0; i < rows * columns; ++i)
		element[i] += x;
	return *this;;
}

template<class T>
matrix<T>& matrix<T>::operator-=(const T& x)
{
	for (int i = 0; i < rows * columns; ++i)
		element[i] -= x;
	return *this;
}

template<class T>
matrix<T>& matrix<T>::operator/=(const T& x)
{
	for (int i = 0; i < rows * columns; ++i)
		element[i] /= x;
	return *this;;
}

template<class T>
matrix<T>& matrix<T>::operator*=(const T& x)
{
	for (int i = 0; i < rows * columns; ++i)
		element[i] *= x;
	return *this;
}
```
## 16
```C++
template<class T>
matrix<T> matrix<T>::tranpose()
{//矩阵的转置
	matrix<T> w(columns, rows);
	for (int i = 0; i < rows * columns; ++i)
		w.element[i / columns + rows * (i % columns)] = element[i];
	return w;
}
```
## 20
> [直接看完整头文件吧，点击跳转](https://www.cnblogs.com/ysjcqs/p/diagonalMatrix.html)
> 后面的其他类的实现暂时跳过了。。。。。。。【官方书籍配套源码里面可能有部分的实现。。。】
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 
```C++

```
## 

```C++

```
## 

```C++

```
## 
```C++

```
