## <span id="1">1</span>
```C++

```
## <span id="2">2</span> 
```C++
template<class T>
void chain<T>::setSize(int theSize)
{
	if (listSize > theSize)
	{
		chainNode<T>* deleteNode;
		for (int i = theSize; i < listSize; ++i)
		{
			chainNode<T>* p = firstNode;
			for (int j = 0; j < theSize - 1; ++j)
				p = p->next;
			deleteNode = p->next;
			p->next = p->next->next;
		}
		delete deleteNode;
		//erase(theSize);
	}
	else
		return;
	listSize = theSize;
}
```
## <span id="3">3</span>
```C++
template<class T>
void chain<T>::set(int theIndex, const T& theElement)
{
	checkIndex(theIndex);

	if (theIndex == 0)
		firstNode->element = theElement;
	else
	{
		chainNode<T>* currentNode = firstNode;
		for (int i = 0; i < theIndex; ++i)
			currentNode = currentNode->next;
		currentNode->element = theElement;
	}
}
```
## <span id="4">4</span> 
```C++
template<class T>
void chain<T>::removeRange(int fromIndex, int toIndex)
{//reomve[fromIndex,toIndex)
	if (fromIndex<0 || toIndex > listSize)
		throw illegalIndex();
	if (toIndex <= fromIndex)
		return;

	chainNode<T>* p = firstNode;
	chainNode<T>* deleteNode;
	int number = toIndex - fromIndex;
	if (fromIndex == 0)
	{
		for (int i = 0; i < number; ++i)
		{
			deleteNode = firstNode;
			firstNode = firstNode->next;
            delete deteleNode;
		}
	}
	else
	{
		for (int i = 0; i < fromIndex - 1; ++i)
			p = p->next;
		for (int i = 0; i < number; ++i)
		{
			deleteNode = p->next;
			p->next = p->next->next;
			delete deleteNode;
		}
	}

	listSize -= number;
}
```
## <span id="5">5</span>
```C++
template<class T>
int chain<T>::lastIndexOf(const T& theElement) const
{
	chainNode<T>* currentNode = firstNode;
	int pos = -1,index = 0;
	do
	{
		if (currentNode->element == theElement)
			pos = index;
		currentNode = currentNode->next;
		++index;
	} while (currentNode !=nullptr);
	return pos;
}
```
## <span id="6">6</span> 
```C++
template<class T>
T& chain<T>::operator[](int theIndex)
{
	return get(theIndex);
}
```
## <span id="7">7</span>
```C++
template<class T>
bool chain<T>::operator==(const chain<T>& rhs)
{
	if (listSize != rhs.listSize)
		return false;
	chainNode<T>* leftNode = firstNode;
	chainNode<T>* rightNode = rhs.firstNode;
	for (int i = 0; i < listSize; ++i)
	{
		if (leftNode->element != rightNode->element)
			return false;
		leftNode = leftNode->next;
		rightNode = rightNode->next;
	}
	return true;
}
```
## <span id="8">8</span> 
```C++
template<class T>
bool chain<T>::operator!=(const chain<T>& rhs)
{
	return !(*this == rhs);
}
```
## <span id="9">9</span>
```C++
template<class T>
bool chain<T>::operator<(const chain<T>& rhs)
{
	bool state;
	chainNode<T>* leftNode = firstNode;
	chainNode<T>* rightNode = rhs.firstNode;
	for (int i = 0; i < listSize && i < rhs.listSize; ++i)
	{
		if (leftNode->element > rightNode->element)
			return false;
		leftNode = leftNode->next;
		rightNode = rightNode->next;
	}
	return true;

}
```
## <span id="10">10</span>
```C++
template<class T>
void chain<T>::swap(chain<T>& theList)
{
	std::swap(listSize, theList.listSize);
	std::swap(firstNode, theList.firstNode);
}
```
## <span id="11">11</span>
```C++

```
## <span id="12">12</span>
```C++

```
## <span id="13">13</span>
```C++

```
## <span id="14">14</span>
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
## <span id="15">15</span>
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

	chainNode<T>* prevNode = firstNode;//前驱
	firstNode = firstNode->next;
	prevNode->next = nullptr;
	chainNode<T>* nextNode = firstNode->next;
	for (int i = 0; i != listSize - 3; ++i)
	{
		firstNode->next = prevNode;
		prevNode = firstNode;
		firstNode = nextNode;
		nextNode = firstNode->next;
	}
	firstNode->next = prevNode;
	nextNode->next = firstNode;
	firstNode = nextNode;
}
```
## <span id="16">16</span> 
```C++
template<class T>
	friend void reverse(chain<T>& theList);


template<class T>
void reverse(chain<T>& theList)
{
	for (int i = 0; i < theList.listSize / 2; ++i)
	{
		//1
		//std::swap(theList.get(i), theList.get(theList.listSize - i - 1));

		//2
		T& lhsElement = theList.get(i);
		T& rhsElement = theList.get(theList.listSize-i-1);
		theList.set(i, rhsElement);
		theList.set(theList.listSize - i - 1,lhsElement);
	}
	//3
	//theList.reverse();
}
```
## <span id="17">17</span>
```C++
template<class T>
void extendedChain<T>::meld(extendedChain<T>& a, extendedChain<T>& b)
{
    clear();
	a.checkIndex(a.size() - 1);
	b.checkIndex(b.size() - 1);
    int minIndex = std::min(a.size(), b.size());
    int index = 0;
    for (; index < minIndex; ++index)
    {
        push_back(a.get(index));
        push_back(b.get(index));
    }
    if (a.size() > b.size())
    {
        for (int i = index; i < a.size(); ++i)
            push_back(a.get(i));
    }
    else if (a.size() < b.size())
    {
        for (int i = index; i < b.size(); ++i)
            push_back(b.get(i));
    }
    listSize = a.size() + b.size();
}
```
## <span id="18">18</span> 
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
## <span id="19">19</span>
```C++
template<class T>
void extendedChain<T>::merge(extendedChain<T>& a, extendedChain<T>& b)
{
	clear();
	a.checkIndex(a.size() - 1);
	b.checkIndex(b.size() - 1);
	chainNode<T>* aNode = a.firstNode;
	chainNode<T>* bNode = b.firstNode;
	while (aNode != nullptr && bNode != nullptr)
	{
		if (aNode->element <= bNode->element)
		{
			push_back(aNode->element);
			aNode = aNode->next;
		}
		else
		{
			push_back(bNode->element);
			bNode = bNode->next;
		}
	}
	if (aNode == nullptr)
	{
		while (bNode != nullptr)
		{
			push_back(bNode->element);
			bNode = bNode->next;
		}
	}
	if (bNode == nullptr)
	{
		while (aNode != nullptr)
		{
			push_back(aNode->element);
			aNode = aNode->next;
		}
	}
	listSize = a.size() + b.size();
}
```
## <span id="20">20</span>
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
## <span id="21">21</span>
```C++
template<class T>
void extendedChain<T>::split(extendedChain<T>& a, extendedChain<T>& b)
{
	a.clear();
	b.clear();
	while (firstNode != nullptr)
	{
		if (firstNode->element & 1)
		{//奇数
			a.push_back(firstNode->element);
			firstNode = firstNode->next;
		}
		else
		{//偶数
			b.push_back(firstNode->element);
			firstNode = firstNode->next;
		}
	}
}
```
## <span id="22">22</span>
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
## <span id="23">23</span>
```C++
template<class T>
void extendedChain<T>::circularShift(int number)
{
    checkIndex(number);
	lastNode->next = firstNode;
	for (int i = 0; i < number ; ++i)
		lastNode = lastNode->next;
	firstNode = lastNode->next;
	lastNode->next = nullptr;
}
```
## <span id="24">24</span>
```C++

```
## <span id="25">25</span>
```C++

```
## <span id="26">26</span>
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
## <span id="27">27</span>
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

template<class T>
void chain<T>::countSort()
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