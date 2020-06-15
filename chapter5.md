## <span id="1">1</span>
```C++
1)false
2)4
3) a,c,异常，异常
4)0,2,-1
5）bcd,abd,abc
6)eabcd,abfcd,abcgd,abcdh,异常，异常
```
## <span id="3">3</span>
```C++
template<class T>
void changeLength2D(T**& a, int oldRows, int oldColumns,
	int newRows, int newColumns)
{
	if (newRows < 0 || newColumns < 0)
		throw illegalParameterValue("new length must be >= 0");
	
	T** temp = new T * [newRows];
	int i;
	for (i = 0; i != newColumns; ++i)
		temp[i] = new T[newColumns];

	int rows = std::min(oldRows, newRows);
	int columns = std::min(oldColumns, newColumns);
	for (i = 0; i != rows; ++i)
		std::copy(a[i], a[i] + columns, temp[i]);

	for (i = 0; i != columns; ++i)
		delete[] a[i];
	delete[] a;
	a = temp;
}
//这里附带官方解答：[https://www.cise.ufl.edu/~sahni/dsaac/public/exer/c5/e3.htm]
```
## <span id="4">4</span> 
```C++
template<class T>
void arrayList<T>::insert(int theIndex, const T& theElement, int spaceSize)
{
	if (theIndex < 0 || theIndex > listSize || spaceSize<listSize)
	{
		std::ostringstream s;
		s << "index = " << theIndex << " size =" << listSize;
		throw illegalIndex(s.str());
	}
	if (listSize == arrayLength)
	{
		changeLength1D(element, arrayLength, spaceSize);
		arrayLength = spaceSize;
	}
	std::copy_backward(element + theIndex, element + listSize, element + listSize + 1);
	element[theIndex] = theElement;
	++listSize;
}
```
## <span id="5">5</span>
```C++
template<class T>
void arrayList<T>::trimToSize()
{
	if (listSize == arrayLength)
		return;
	ir(listSize == 0)
	{
		delete[] element;
		element = new T[1];
		arrayLength = 1;
		return;
	}

	changeLength1D(element, listSize, listSize);
	arrayLength = listSize;
}
//复杂度：O(listSize)
```
## <span id="6">6</span> 
```C++
template<class T>
void arrayList<T>::setSize(int newSize)
{
	if (newSize <= listSize)
		return;
	changeLength1D(element, listSize, newSize);
	arrayLength = newSize;
}
//复杂度：O(newSize)
```
## <span id="7">7</span>
```C++
template<class T>
T& arrayList<T>::operator[](int index)
{
	checkIndex(index);
	return element[index];
}
```
## <span id="8">8</span> 
```C++
//类内声明
template<class T>
	friend bool operator==(const arrayList<T>& lhs, const arrayList<T>& rhs);
//实现
template<class T>
bool operator==(const arrayList<T>& lhs, const arrayList<T>& rhs)
{
	if (lhs.listSize != rhs.listSize)
		return false;
	for (int i = 0; i != lhs.listSize; ++i)
		if (lhs.element[i] != rhs.element[i])
			return false;
	return true;
}
//非友元
template<class T>
 bool arrayList<T>::operator==(const arrayList<T>& rhs)
{
	if (listSize != rhs.listSize)
		return false;
	for (int i = 0; i != listSize; ++i)
		if (element[i] != rhs.element[i])
			return false;
	return true;
}
```
## <span id="9">9</span>
```C++
//友元
template<class T>
bool operator!=(const arrayList<T>& lhs, const arrayList<T>& rhs)
{
	return !(lhs == rhs);//需先重载operator==
}
//非友元
template<class T>
 bool arrayList<T>::operator!=(const arrayList<T>& rhs)
{
	return !(*this == rhs);
}
```
## <span id="10">10</span>
```C++
template<class T>
 bool arrayList<T>::operator<(const arrayList<T>& rhs)
{
	bool state = true;
	for (int i = 0; i != listSize && i != rhs.listSize; ++i)
		if (this->element[i] > rhs.element[i])
			state = false;
	return state;
}
```
## <span id="11">11</span>
```C++
template<class T>
 void arrayList<T>::push_back(const T& theElement)
{
	if (listSize == arrayLength)
	{
		changeLength1D(element, listSize, 2 * arrayLength);
		arrayLength *= 2;
	}
	element[listSize] = theElement;
	++listSize;
}
```
## <span id="12">12</span>
```C++
template<class T>
 void arrayList<T>::pop_bake()
{
	element[--listSize].~T();
}
```
## <span id="13">13</span>
```C++
template<class T>
 void arrayList<T>::swap(arrayList<T>& theList)
{
	std::swap(listSize, theList.listSize);
	std::swap(arrayLength, theList.arrayLength);
	std::swap(element,theList.element);
}
//O(1)
```
## <span id="14">14</span>
```C++
...
template<class T>
 void arrayList<T>::reserve(int theCapacity)
{
	int old = arrayLength;
	arrayLength = std::max(old, theCapacity);
	if (old == arrayLength)
		return;
	else
		changeLength1D(element, arrayLength, theCapacity);
}
...
    
int main()
{
	arrayList<int> a(3);
	std::cout << a.capacity() << std::endl;
	a.reserve(4);
	std::cout << a.capacity() << std::endl;
	a.reserve(5);
	std::cout << a.capacity() << std::endl;
	a.reserve(4);
	std::cout << a.capacity() << std::endl;
	return 0;
}
```
## <span id="15">15</span>
```C++
template<class T>
 void arrayList<T>::set(int theIndex, const T& theElemenet)
{
	checkIndex(theIndex);
	element[theIndex] = theElemenet;
}
```
## <span id="16">16</span> 
```C++
template<class T>
 void arrayList<T>::clear()
{
	for (int i = 0; i < listSize; ++i)
		element[i].~T();
	listSize = 0;
}
```
## <span id="17">17</span>
```C++
template<class T>
 void arrayList<T>::removeRange(int start, int end)
{
	if (start<0 || end>listSize)
		throw illegalIndex();
	if (start >= end)
		return;
	std::copy(element + end, element + listSize, element + start);
	int newSize = listSize - end + start;
	for (int i = newSize; i < listSize; ++i)
		element[i].~T();
	std::cout << "element :" << element[newSize] << std::endl;
	listSize  = newSize;
}
```
## <span id="18">18</span> 
```C++
template<class T>
 int arrayList<T>::lastIndexOf(const T& theElement) const
{
	int theIndex, thePos = -1;
	do
	{
		theIndex = thePos;
		thePos =
		(int)(std::find(element + theIndex + 1, 
			element + listSize, theElement) - element);

	} while (thePos != listSize);
	return  (theIndex == listSize) ? -1 : theIndex;
}
```
## <span id="19">19</span>
```C++

```
## <span id="20">20</span>
```C++
1)
template<class T>
 void arrayList<T>::removedSize(int initialCapacity)
{
	if (listSize <= (arrayLength / 4))
		changeLength1D(element, arrayLength, std::max(arrayLength / 2, initialCapacity));
}
```
## <span id="21">21</span>
```C++

```
## <span id="22">22</span>
```C++
1)
//24题需要有参转置，见24
template<class T>
 void arrayList<T>::reverse()
{
	int k = 0;
	while (k < listSize / 2)
	{
		std::swap(element[k], element[listSize - k - 1]);
		++k;
	}
}
4)
template<class T>
	friend void fReverse(arrayList<T>& theList) { theList.reverse(); }
//main() -> fReverse(a);
```
## <span id="23">23</span>
```C++
template<class T>
 void arrayList<T>::leftShift(int i)
{
	std::copy(element + i, element + listSize, element);
	for (int index = listSize - i; index != listSize; ++index)
		element[index].~T();
	listSize = listSize - i;
}

//main()
int main()
{
	arrayList<int> a(3);
	a.insert(0, 1);
	a.insert(1, 2);
	a.insert(2, 3);
	a.push_back(2);
	a.push_back(5);
	a.output(std::cout);
	a.leftShift(2);
	a.output(std::cout);
	return 0;
}
```
## <span id="24">24</span>
```C++
template<class T>
 void arrayList<T>::reverse(int first, int end)
{//注意reverse[frist,end)
	while (first < (first + end) / 2)
	{
		--end;
		std::swap(element[first], element[end]);
		++first;
	}
}

template<class T>
 void arrayList<T>::circularShift(int i)
{//把element拆解成两个以i为界限序列
	//注意reverse[frist,end)
	reverse(0, i);
	reverse(i, listSize );
	reverse(0, listSize );
}
```
## <span id="25">25</span>
```C++
template<class T>
 void arrayList<T>::half()
{
	for (int i = 0; i < listSize; i += 2)
		element[i / 2] = element[i];
	int newSize = (listSize + 1) / 2;
	for (int i = newSize; i < listSize; ++i)
		element[i].~T();
	listSize = newSize;
}
```
## <span id="26">26</span>
```C++

```
## <span id="27">27</span>
```C++
template<class T>
class arrayList : public linearList<T>
{
public:
    ...
	class iterator;
	iterator begin() { return iterator(element); }
	iterator end() { return iterator(element + listSize); }
    
	class iterator
    {
      ...  
    };
    ...
};


//main
int main()
{
	arrayList<int> a(3);
	a.insert(0, 1);
	a.insert(1, 2);
	a.insert(2, 3);
	a.push_back(4);
	a.push_back(5);
	for (arrayList<int>::iterator it = a.begin();
		it != a.end(); ++it)
		cout << *it << " ";
	cout << endl;
	return 0;
}
```
## <span id="28">28</span>
```C++
template<class T>
void arrayList<T>::meld( arrayList<T>& a,  arrayList<T>& b)
{
	delete[] element;
	listSize = a.size() + b.size();
	arrayLength = listSize;
	element = new T[listSize];

	int minIndex = std::min(a.size(), b.size());
	int index = 0;
	for (int i = 0; i < minIndex; ++i)
	{
		element[index++] = a.get(i);
		element[index++] = b.get(i);
	}

	arrayList<T>::iterator beg, end;
	if (a.size() < b.size())
	{
		beg = b.begin() + minIndex;//注意 需重载iterator+  而不是++
		end = b.end();
	}
	else if (a.size() > b.size())
	{
		beg = a.begin() + minIndex;
		end = a.end();
	}
	arrayList<T>::iterator to = begin() + 2 * minIndex;
	std::copy(beg, end, to);
}
//重载
iterator& operator+(int index) { position+=index; return *this; }
```
## <span id="29">29</span>
```C++
template<class T>
void arrayList<T>::merge(arrayList<T>& a, arrayList<T>& b)
{
	delete[] element;
	listSize = a.size() + b.size();
	arrayLength = listSize;
	element = new T[listSize];

	int ca = 0;                       
	int cb = 0;                       
	int ct = 0;                       

	while ((ca < a.listSize) && (cb < b.listSize))
		if (a.element[ca] <= b.element[cb])
			element[ct++] = a.element[ca++];
		else
			element[ct++] = b.element[cb++];

	std::copy(a.element + ca, a.element + a.listSize, element + ct);
	ct += a.listSize - ca;
	std::copy(b.element + cb, b.element + b.listSize, element + ct);
	ct += b.listSize - cb;
}
```
## <span id="30">30</span>
```C++
template<class T>
void arrayList<T>::split(arrayList<T>& a, arrayList<T>& b)
{
	a.clear();
	b.clear();
	for (int i = 0; i < listSize; ++i)
		if (element[i] & 1)
			a.push_back(element[i]);
		else
			b.push_back(element[i]);
}
```
## <span id="31">31</span>
```C++
官方：【https://www.cise.ufl.edu/~sahni/dsaac/public/exer/c5/e31.htm】
Data Structures, Algorithms, & Applications in C++
Chapter 5, Exercise 31

The code is given below and in the file arrayCircularList.h. Test code is included in arrayCircularList.cpp.
template<class T>
class circularArrayList : public linearList<T> 
{
   public:
      // constructor, copy constructor and destructor
      circularArrayList(int initialCapacity = 10);
      circularArrayList(const circularArrayList<T>&);
      ~circularArrayList() {delete [] element;}

      // ADT methods
      bool empty() const {return first == -1;}
      int size() const
         {if (first == -1)
             return 0;
          else
             return (arrayLength + last - first) % arrayLength + 1;
         }
      T& get(int theIndex) const;
      int indexOf(const T& theElement) const;
      void erase(int theIndex);
      void insert(int theIndex, const T& theElement);
      void output(ostream& out) const;

      // additional method
      int capacity() const {return arrayLength;}

   protected:
      void checkIndex(int theIndex) const;
            // throw illegalIndex if theIndex invalid
      T* element;            // 1D array to hold list elements
      int arrayLength;       // capacity of the 1D array
      int first;             // location of first element
      int last;              // location of last element
};

template<class T>
circularArrayList<T>::circularArrayList(int initialCapacity)
{// Constructor.
   if (initialCapacity < 1)
   {ostringstream s;
    s << "Initial capacity = " << initialCapacity << " Must be > 0";
    throw illegalParameterValue(s.str());
   }
   arrayLength = initialCapacity;
   element = new T[arrayLength];
   first = -1;   // list is empty
}

template<class T>
circularArrayList<T>::circularArrayList(const circularArrayList<T>& theList)
{// Copy constructor.
   arrayLength = theList.arrayLength;
   element = new T[arrayLength];
   first = theList.first;
   if (first == -1)
      return;   // theList is empty
  
   // non-empty list
   last = theList.last;
   int current = first;
   while (current != last)
   {
      element[current] = theList.element[current];
      current = (current + 1) % arrayLength;
   }
   element[current] = theList.element[current];
}

template<class T>
void circularArrayList<T>::checkIndex(int theIndex) const
{// Verify that theIndex is between 0 and size() - 1.
   int listSize = size();
   if (theIndex < 0 || theIndex >= listSize)
   {ostringstream s;
    s << "index = " << theIndex << " size = " << listSize;
    throw illegalIndex(s.str());
   }
}

template<class T>
T& circularArrayList<T>::get(int theIndex) const
{// Return element whose index is theIndex.
 // Throw illegalIndex exception if no such element.
   checkIndex(theIndex);
   return element[(first + theIndex) % arrayLength];
}

template<class T>
int circularArrayList<T>::indexOf(const T& theElement) const
{// Return index of first occurrence of theElement.
 // Return -1 if theElement not in list.

   int listSize = size();
   for (int i = 0; i < listSize; i++)
      if (element[(first + i) % arrayLength] == theElement)
         return i;

   return -1;
}

template<class T>
void circularArrayList<T>::erase(int theIndex)
{// Delete the element whose index is theIndex.
 // Throw illegalIndex exception if no such element.
   checkIndex(theIndex);

   // no exception thrown, valid index, remove element
   if (size() == 1)
   {// list becomes empty
      element[first].~T();   // delete element
      first = -1;
      return;
   }

   // determine which side has fewer elements
   // and shift the smaller number of elements
   int listSize = size();
   if (theIndex <= (listSize - 1) / 2)
   {// shift elements theIndex - 1 ... 0
      for (int i = theIndex - 1; i >= 0; i--)
          element[(first + i + 1) % arrayLength]
             = element[(first + i) % arrayLength];
      element[first].~T();    // delete
      first = (first + 1) % arrayLength;
   }
   else
   {// shift elements theIndex + 1 ... size() - 1
      for (int i = theIndex + 1; i < listSize; i++)
          element[(first + i - 1) % arrayLength]
             = element[(first + i) % arrayLength];
      element[last].~T();   // delete
      last = (arrayLength + last - 1) % arrayLength;
   }
}

template<class T>
void circularArrayList<T>::insert(int theIndex, const T& theElement)
{// Insert theElement so that its index is theIndex.
   int listSize = size();
   if (theIndex < 0 || theIndex > listSize)
   {// invalid index
      ostringstream s;
      s << "index = " << theIndex << " size = " << listSize;
      throw illegalIndex(s.str());
   }

   // valid index, handle empty list as special case
   if (first == -1)
   {// insert into empty list
      first = last = 0;
      element[0] = theElement;
      return;
   }

   // insert into a nonempty list, make sure we have space
   if (listSize == arrayLength)
   {// no space, double capacity
      T* newArray = new T [2 * arrayLength];

      // copy elements into new array beginning at position  0
      int j = 0;   // position in newArray to copy to
      for (int i = first;
               i != last; i = (i + 1) % arrayLength)
         newArray[j++] = element[i];
      newArray[j] = element[last];  // copy last element

      // switch to newArray and set first and last
      delete [] element;
      element = newArray;
      arrayLength *= 2;
      first = 0;
      last = j;
   }

   // create space for new element
   if (theIndex <= listSize / 2)
   {// shift elements 0 through theIndex - 1
      for (int i = 0; i < theIndex; i++)
         element[(arrayLength + first + i - 1) % arrayLength]
             = element[(first + i) % arrayLength];
      first = (arrayLength + first - 1) % arrayLength;
   }
   else
   {// shift elements listSize - 1  ... theIndex
      for (int i = listSize - 1; i >= theIndex; i--)
         element[(first + i + 1) % arrayLength]
              = element[(first + i) % arrayLength];
      last = (last + 1) % arrayLength;
   }
       
   // insert new element
   element[(first + theIndex) % arrayLength] = theElement;
}

template<class T>
void circularArrayList<T>::output(ostream& out) const
{// Put the list into the stream out.
   if (first == -1)
      return;   // list is empty
   
   // non-empty list
   int current = first;
   while (current != last)
   {
      cout << element[current]  << "  ";
      current = (current + 1) % arrayLength;
   }
   cout << element[current]  << "  ";
}

// overload <<
template <class T>
ostream& operator<<(ostream& out, const circularArrayList<T>& x)
   {x.output(out); return out;}
The complexity of each method is the same as that of the corresponding method of arrayList.
```