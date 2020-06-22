# 声明

- 内容根据数据结构、算法与应用C++描述书籍练习题的实现，实现普通链表的插入，选择，冒泡，计数排序，交叉排序，奇偶交叉以及归并排序,链表的反转,循环元素移动，网上也有其他解答，由于新人刚学习算法。方法实现很笨，可能存在各种问题，网上这些方法很多，我只是记录一下自己的方法。DeBug的日常！！！
- [书籍习题汇总](https://www.cnblogs.com/ysjcqs/p/DataChapter.html)
- [数组描述排序](https://www.cnblogs.com/ysjcqs/p/Sort.html)

# 前置条件

```C++
template<class T>
struct chainNode
{
	T element;
	chainNode<T>* next;

	chainNode() {}
	chainNode(const T& element) { this->element = element; }
	chainNode(const T& element, chainNode<T>* next)
	{
		this->element = element;
		this->next = next;
	}
};

//普通链表
template<class T>
class chain : public linearList<T>
{
public:
    ...
    void leftShift(int i);
    void reverse();
	void meld(chain<T>& a, chain<T>& b);
	void merge(chain<T>& a, chain<T>& b);
	void split(chain<T>& a, chain<T>& b);
    void insertSort();
	void bubbleSort();
	void selectSort();
	void countSort();
    ...
protected:
	chainNode<T>* firstNode;
	int listSize;
};

//多调试，知其用
```

# 插入排序

```C++
template<class T>
void chain<T>::insertSort()
{
	if (!firstNode || !firstNode->next)
		return;
	chainNode<T>* dummyNode = new chainNode<T>(INT_MIN);
	chainNode<T>* prevNode, * currNode, * tempNode;
	dummyNode->next = firstNode;
	prevNode = firstNode;
	currNode = firstNode->next;
	while (currNode != nullptr)
	{
		if (currNode->element < prevNode->element)
		{
			tempNode = dummyNode;
			while (tempNode->next->element < currNode->element)
			{
				tempNode = tempNode->next;
			}
			prevNode->next = currNode->next;
			currNode->next = tempNode->next;;
			tempNode->next = currNode;
			currNode = prevNode->next;
		}
		else
		{
			prevNode = prevNode->next;
			currNode = currNode->next;
		}
	}
	firstNode = dummyNode->next;
}
```



# 冒泡排序

```C++
template<class T>
void chain<T>::bubbleSort()
{
	if (!firstNode || !firstNode->next)
		return;
	chainNode<T>* dummyNode, * prevNode, * currNode, * tailNode, * tempNode;
	dummyNode = new chainNode<T>(-1, firstNode);
	prevNode = dummyNode->next;
	currNode = prevNode->next;
	tailNode = firstNode->next;
	while (tailNode != nullptr)
		tailNode = tailNode->next;

	while (prevNode->next != tailNode)
	{
		tempNode = dummyNode;
		while (currNode != tailNode)
		{
			if (currNode->element < prevNode->element)
			{
				prevNode->next = currNode->next;
				currNode->next = prevNode;
				tempNode->next = currNode;
				tempNode = tempNode->next;
				currNode = prevNode->next;
			}
			else
			{
				prevNode = prevNode->next;
				currNode = currNode->next;
				tempNode = tempNode->next;
			}
		}
		tailNode = prevNode;
		prevNode = dummyNode->next;
		currNode = prevNode->next;
	}
	firstNode = dummyNode->next;
}
```



# 选择排序

```C++
template<class T>
void chain<T>::selectSort()
{
	if (!firstNode || !firstNode->next)
		return;
	chainNode<T>* maxNode, * maxPrevNode;
	chainNode<T>* currNode, * currPrevNode;
	chainNode<T>* dummyNode, * tailNode;
	dummyNode = maxPrevNode = currPrevNode = new chainNode<T>(INT_MIN, firstNode);
	currNode = maxNode = firstNode;
	tailNode = firstNode->next;
	while (tailNode != nullptr)
		tailNode = tailNode->next;;

	while (maxNode->next != tailNode)
	{
		while (currNode->next != tailNode)
		{
			if (maxNode->element < currNode->element)
			{
				maxNode = currNode;
				maxPrevNode = currPrevNode;
			}
			currNode = currNode->next;
			currPrevNode = currPrevNode->next;
		}
		currPrevNode->next = maxNode;
		maxPrevNode->next = currNode;
		currNode->next = maxNode->next;
		maxNode->next = tailNode;

		//初始化尾节点和firstNode
		tailNode = maxNode;
		firstNode = dummyNode->next;

		//初始化新一轮状态
		maxNode = dummyNode->next;
		currNode = maxNode->next;
		maxPrevNode = dummyNode;
		currPrevNode = maxPrevNode->next;
	}
}
```



# 计数排序

[参考](https://blog.csdn.net/Jeff_Winger/article/details/78303386?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-13.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromBaidu-13.nonecase 参考)



```C++
template<class T>
inline void chain<T>::countSort()
{
	if (!firstNode || !firstNode->next)
		return;
	chainNode<T>* p, * pr;
	chainNode<T>* dummyNode = new chainNode<T>(INT_MIN, firstNode);
	p = firstNode->next;
	int* r = new int[listSize];
	for (int i = 0; i < listSize; ++i)
		r[i] = 0;
	int i = 1, j = 0;
	while (p!=nullptr)
	{
		pr = dummyNode->next;
		j = 0;
		while (pr!=p)
		{
			if (pr->element <= p->element)
				++r[i];
			else
				++r[j];
			pr = pr->next;
			++j;
		}
		p = p->next;
		++i;
	}

	chainNode<T>* pb = dummyNode->next;
	int k = 0, t;
	T temp;
	while (pb!=nullptr)
	{
		int i = 0;
		chainNode<T>* pd = dummyNode->next;
		while (k!=r[i])
		{
			pd = pd->next;
			++i;
		}
		if (k != r[k])
		{
			temp = pb->element;
			pb->element = pd->element;
			pd->element = temp;
			t = r[i];
			r[i] = r[k];
			r[k] = t;
		}
		pb = pb->next;
		++k;
	}
	delete[] r;
}
```

# 交叉

```C++
template<class T>
void chain<T>::meld(chain<T>& a, chain<T>& b)
{
	a.checkIndex(a.size() - 1);
	b.checkIndex(b.size() - 1);
	int minIndex = std::min(a.size(), b.size());
	int index = 0;
	chainNode<T>* aNode;
	chainNode<T>* bNode;
	chainNode<T>* cNode;
	chainNode<T>* tempNode;

	firstNode = a.firstNode;
	aNode = a.firstNode->next;
	firstNode->next = b.firstNode;
	bNode = b.firstNode->next;
	cNode = firstNode->next;

	for (; index < minIndex - 1; ++index)
	{
		cNode->next = aNode;
		tempNode = aNode->next;
		aNode->next = bNode;
		aNode = tempNode;
		cNode = bNode;
		bNode = bNode->next;
	}
	if (a.size() > b.size())
	{
		while (aNode != nullptr)
		{
			cNode->next = aNode;
			aNode = aNode->next;
			cNode = cNode->next;
		}
	}
	else if (a.size() < b.size())
	{
		while (bNode != nullptr)
		{
			cNode->next = bNode;
			bNode = bNode->next;
			cNode = cNode->next;
		}
	}
	a.firstNode = nullptr;
	b.firstNode = nullptr;
	listSize = a.size() + b.size();
}
```

# 奇偶交叉

```C++
template<class T>
void chain<T>::split(chain<T>& a, chain<T>& b)
{
	chainNode<T>* aNode = nullptr;
	chainNode<T>* bNode = nullptr;

	while (firstNode != nullptr)
	{
		if (firstNode->element & 1)
		{
			if (a.size() == 0)
			{
				aNode = a.firstNode = firstNode;
				firstNode = firstNode->next;
				++a.listSize;
				continue;
			}
			aNode->next = firstNode;
			firstNode = firstNode->next;
			aNode = aNode->next;
			aNode->next = nullptr;
			++a.listSize;
		}
		else
		{
			if (b.size() == 0)
			{
				bNode = b.firstNode = firstNode;
				firstNode = firstNode->next;
				++b.listSize;
				continue;
			}
			bNode->next = firstNode;
			firstNode = firstNode->next;
			bNode = bNode->next;
			bNode->next = nullptr;
			++b.listSize;
		}
	}
}
```

# 归并

```C++
template<class T>
void chain<T>::merge(chain<T>& a, chain<T>& b)
{
	a.checkIndex(a.size() - 1);
	b.checkIndex(b.size() - 1);

	chainNode<T>* aNode = a.firstNode;
	chainNode<T>* bNode = b.firstNode;
	chainNode<T>* cNode = firstNode;

	if (aNode->element <= bNode->element)
	{
		firstNode = cNode = aNode;
		aNode = aNode->next;
	}
	else
	{
		firstNode = cNode = bNode;
		bNode = bNode->next;
	}

	while (aNode != nullptr && bNode != nullptr)
	{
		if (aNode->element <= bNode->element)
		{
			cNode->next = aNode;
			cNode = cNode->next;
			aNode = aNode->next;
		}
		else
		{
			cNode->next = bNode;
			cNode = cNode->next;
			bNode = bNode->next;
		}
	}
	if (aNode == nullptr)
	{
		while (bNode != nullptr)
		{
			cNode->next = bNode;
			cNode = cNode->next;
			bNode = bNode->next;
		}
	}
	if (bNode == nullptr)
	{
		while (aNode != nullptr)
		{
			cNode->next = aNode;
			cNode = cNode->next;
			aNode = aNode->next;
		}
	}
	a.firstNode = nullptr;
	b.firstNode = nullptr;
	listSize = a.size() + b.size();
}
```

# 反转

```C++
template<class T>
void chain<T>::reverse()
{
	if (listSize < 2)
		return;
	if (listSize == 2)
	{
		chainNode<T>* tempNode = firstNode;
		firstNode = firstNode->next;
		firstNode->next = tempNode;
		tempNode->next = nullptr;
		return;
	}

	chainNode<T>* preNode = firstNode;
	firstNode = firstNode->next;
	preNode->next = nullptr;
	chainNode<T>* nextNode = firstNode->next;
	for (int i = 0; i != listSize - 3; ++i)
	{
		firstNode->next = preNode;
		preNode = firstNode;
		firstNode = nextNode;
		nextNode = firstNode->next;
	}
	firstNode->next = preNode;
	nextNode->next = firstNode;
	firstNode = nextNode;
}
```

# 循环元素移动

```C++
template<class T>
void chain<T>::leftShift(int number)
{
	chainNode<T>* deleteNode;
	for (int i = 0; i < number; ++i)
	{
		deleteNode = firstNode;
		firstNode = firstNode->next;
		delete deleteNode;
	}
	listSize -= number;
}
```

