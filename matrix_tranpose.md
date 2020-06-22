# 矩阵的转置

> 转置用一维数组描述的二维矩阵。如若是二维数组的转置。可以考虑二维转一维在转置。。。当然，你愿意的话。。。（数据结构、算法与应用C++描述第七章习题）

> [习题汇总](https://www.cnblogs.com/ysjcqs/p/DataChapter.html)

# matrix类

```C++
template<class T>
class matrix
{
	friend std::ostream& operator<<
		(std::ostream& out, const matrix<T>& theMatrix);
public:
	...
	matrix<T> tranpose();
    T& operator() (int i, int j) const;//类似数学中的访问
	...

private:
	int rows, columns;
	T* element;
};


//转置实现
template<class T>
matrix<T> matrix<T>::tranpose()
{
	matrix<T> w(columns, rows);
    //用i遍历完一维数组,利用除法和求余锁定步长
	for (int i = 0; i < rows * columns; ++i)
		w.element[i / columns + rows * (i % columns)] = element[i];
	return w;
}
```

# 测试

```C++
#include <iostream>
#include "matrix.h"

using namespace std;
int main()
{
    try
    {
        matrix<int> x(3, 2), y, z;
        int i, j;
        for (i = 1; i <= 3; i++)
            for (j = 1; j <= 2; j++)
                x(i, j) = 2 * i + j;
        cout << "Initialized x(i,j) = 2*i + j" << endl;
        cout << "x(3,1) = " << x(3, 1) << endl;
        cout << "x is" << endl;;
        cout << x << endl;

        y = x.tranpose();
        cout << y << endl;
    }
    catch (...) {
        cerr << "An exception has occurred" << endl;
    }

    return 0;
}
```

# 输出

```C++
Initialized x(i,j) = 2*i + j
x(3,1) = 7
x is
3  4
5  6
7  8

3  5  7
4  6  8
```

