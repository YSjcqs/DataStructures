#include <iostream>

template<typename T>
void countSort(T a[], int n, int r[])
{//计数排序
	int i;
	for (i = 0; i < n; ++i)		//初始化
		r[i] = 0;

	for (i = 0; i < n; ++i)		//计算名次
		for (int j = 0; j < i; ++j)
			if (a[j] <= a[i]) ++r[i];
			else ++r[j];

	T* u = new T[n];

	for (i = 0; i < n; ++i)		//依照名次把a的值放在正确的位置
		u[r[i]] = a[i];
	for (i = 0; i < n; ++i)		//吧u中的值移会a中
		a[i] = u[i];
	delete[] u;
}

template<typename T>
void rearrange(T a[], int n, int r[])
{//原地重排
	int i;
	for (i = 0; i < n; ++i)		//初始化
		r[i] = 0;

	for (i = 0; i < n; ++i)		//计算名次
		for (int j = 0; j < i; ++j)
			if (a[j] <= a[i]) ++r[i];
			else ++r[j];

	for (int i = 0; i < n; ++i)
		while (r[i]!=i)
		{
			std::swap(a[i], a[r[i]]);
			std::swap(r[i], r[r[i]]);
		}
}

template<typename T>
void selectionSort(T a[], int n)
{//选择排序
	int maxVal, i, j;
	for (i = n - 1; i > 0; --i)
	{//排序
		maxVal = i;
		for (j = 0; j < i; ++j)
		{//找出最大的值
			if (a[maxVal] < a[j])
				maxVal = j;
		}
		std::swap(a[i], a[maxVal]);
	}
}

template<typename T>
void bubbleSort(T a[], int n)
{//冒泡排序
	for (int i = n - 1; i > 0; --i)
		for (int j = 0; j < i; ++j)	//把最大值移到右边
			if (a[j] > a[j+1])
				std::swap(a[j], a[j+1]);
}

template<typename T>
void insertSort(T a[], int n)
{//插入排序
	for (int i = 1; i < n; ++i)
	{
		T t = a[i];
		int j;
		for (j = i - 1; j >= 0 && t < a[j]; --j)
			a[j + 1] = a[j];
		a[j + 1] = t;
	}
}


template<typename T>
void selectionSort(T a[], int n)
{//及时终止选择排序
	int maxVal, i, j;
	bool sorted = false;
	for (i = n - 1; !sorted && (i > 0); --i)
	{//排序
		maxVal = 0;
		sorted = true;
		for (j = 1; j < i + 1; ++j)
		{//找出最大的值
			if (a[maxVal] <= a[j])	maxVal = j;
			else sorted = false;
		}
		std::swap(a[i], a[maxVal]);
	}
}

template<typename T>
void bubbleSort(T a[], int n)
{//及时终止冒泡排序
	bool swapped = false;
	for (int i = n - 1; i > 0 && !swapped; --i)
	{
		swapped = true;
		for (int j = 0; j < i; ++j)	//把最大值移到右边
			if (a[j] > a[j + 1])
			{
				std::swap(a[j], a[j + 1]);
				swapped = false;
			}
	}
}
 
int main()
{
	int a[]{ 6,5,8,4,3,1 };
	int r[5];
	//countSort(a, 5, r);
	rearrange(a, 6, r);
	//selectionSort(a, 6);
	//bubbleSort(a, 6);
	insertSort(a, 6);
	for (auto e : a)
		std::cout << e << " ";
	std::cout << std::endl;
	return 0;
}