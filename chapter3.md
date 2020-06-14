## <span id="1">1</span>
```C++
(a)
lim n -> infinity (q(n) / p(n))
= lim n -> infinity (100n2 + 6)/(3n4 + 2n2)
= lim n -> infinity (100/n2 + 6/n4)/(3 + 2/n2)
= 0/3
= 0


(c)
lim n -> infinity (q(n) / p(n))
= lim n -> infinity 10n2/(7n2log n)
= lim n -> infinity (10/log n)/7
= 0/7
= 0
```
## <span id="2">2</span> 
```C++
(a)
O(n3)

(c)
O(n2log n)

(e)
O(n2n)
```
## <span id="3">3</span>
```C++
(a)
2n + 7渐近地大于1。因此，2n + 7 != O(1)。
(c)
5n3 + 6n2渐近大于n2。因此，5n3 + 6n2 != O(n2)。
```
## <span id="4">4</span> 
```C++
(a)
Omega(n3)

(c)
Omega(n2log n)

(e)
Omega(n2n)
```
## <span id="5">5</span>
```C++
(a)
2n + 7渐近地小于n2。因此，2n + 7 != (n2)
(c)
5n3 + 6n2渐近小于n3log n，因此，5n3 + 6n2 != (n3log n)
```
## <span id="6">6</span> 
```C++
(a)
Theta(n3)

(c)
Theta(n2log n)

(e)
Theta(n2n)
```
## <span id="7">7</span>
```C++
(a)
t(n) = Theta(1)

(c)
t(n) = Theta(n2)

(e)
t(n) = Omega(n3)

(g)
t(n) = Theta(n2)
```
## <span id="8">8</span> 
```C++
(a)
Theta(m2n2+m3n)

(c)
Theta(m4+n3+m3n2)
```
## <span id="9">9</span>
```C++
(a)
5n2 - 6n < 5n2 for n >= 1. So, 5n2 - 6n = O(n2). Also, 5n2 - 6n >= 5n2 - n2 = 4 n2 for n >= 6. So, 5n2 - 6n = Omega(n2). Consequently, 5n2 - 6n = Theta(n2).

(c)
f(n) = 2n22n + n log n < 2n22n + n2 < 3n22n for n >= 1. So, f(n) = O(n22n). Also, f(n) >= 2n22n for n >= 1. So, f(n) = Omega(n22n). Therefore, f(n) = Theta(n22n).

(e)
f(n) = sum from (i=0) to n i3 <= sum from (i=1) to n n3 = n4 for n >= 1. So, f(n) = O(n4). Also, f(n) >= sum from (i=ceil(n/2)) to n i3 >= sum from (i=ceil(n/2)) to n (n/2)3 = (n - ceil(n/2) + 1)(n/2)3 >= n4/16 for n >= 1. So, f(n) = Omega(n4). As a result, f(n) = Theta(n4).

(g)
f(n) = n3 + 106n2 <= n3 + n3 = 2 n3 for n >= 106. Also, f(n) < n3 for n > 0. So, f(n) = Theta(n3).
```
## <span id="10">10</span>
```C++
(a)
(5n2 - 6n) / n2 = 5 - 6 / n which is <= 5. n2 / (5n2 - 6n) = n / (5n - 6) = 1 / (5 - 6 / n) which, in the limit, is <= 1 / 4. So, the function is Theta(n2).

(c)
f(n) / g(n) = 2 + (log n) / (n 2n) < 3. g(n) / f(n) = 1 / (2 + (log n / (n 2n)) <= 0.5. So, f(n) = Theta(g(n)).

(e)
f(n) / g(n) = [sum from (i=0) to n i3] / n4 <= [sum from (i=1) to n n3] / n4 = n4 / n4 = 1. Consider the case when n is even. g(n) / f(n) <= n4 / (sum from (i = n / 2 + 1) to n i3) < n4 / (sum from (i = n / 2 + 1) to n (n / 2)3) = n4 / (n4 / 16) = 16. The proof that g(n) / f(n) <= c when n is odd is similar. So, f(n) = Theta(g(n)).

(g)
f(n) / g(n) = 1 + 106 / n <= 106 + 1 and g(n) / f(n) <= 1. Hence, f(n) = Theta(g(n)).
``` 
## <span id="11">11</span>
```C++
(a)
f(n) / g(n) = 10n + 9 / n which goes to infinity as n goes to infinity. So, f(n) is not O(g(n)).

(c)
g(n) / f(n) = log n which goes to infinity as n goes to infinity. So, f(n) is not Theta(g(n)).
```

## <span id="13">13</span>
```C++
If f(n) = Omega(g(n)), then there exist a positive c and an n0 such that g(n)/f(n) <= c for all n >= n0. Hence, the limit of g(n)/f(n) as n goes to infinity is <= c. Next, suppose that the limit of g(n)/f(n) as n goes to infinity is <= c. From this it follows that there is an n0 such that g(n) <= max{1, c} * f(n) for all n >= n0. This proves Theorem 3.4. Theorems 3.2 and 3.4 together imply Theorem 3.6.
```
 
## <span id="15">15</span>
```C++
(E5)
(sum from 1 to n)ik <= (sum from 1 to n)nk = nk+1. Therefore, (sum from 1 to n)ik = O(nk+1). Further, (sum from 1 to n)ik >= (sum from n/2 to n)(n/2)k = (n/2)k+1. Therefore, (sum from 1 to n)ik = Omega(nk+1). (Note that 2k+1 is a constant as k is a constant.) Consequently, (sum from 1 to n)ik = Theta(nk+1).

(E6)
(sum from 1 to n)ri = (rn+1-1)/(r-1) - 1 = Theta(rn). From this it follows that (sum from 1 to n)ri = O(rn) and (sum from 1 to n)ri = Omega(rn).
```

## <span id="17">17</span>
```C++
(a)
Not true. For example, if f(n) = n2 and g(n) = 1, then f(n) = O(n2) and g(n) = O(n2). But, f(n)/g(n) = n2 != O(1).

(b)
Not true. For example, if f(n) = n2 and g(n) = n2, then f(n) = O(n4) and g(n) = O(n2). But, f(n)/g(n) = 1 != Omega(n2).

(c)
Not true. Follows from (a) and/or (b).

(d)
Not true. For example, if f(n) = n2 and g(n) = n2, then f(n) = Omega(n2) and g(n) = Omega(1). But, f(n)/g(n) = 1 != Omega(n2).

(e)
Not true. For example, if f(n) = n2 and g(n) = 1, then f(n) = Omega(1) and g(n) = Omega(1). But, f(n)/g(n) = n2 != O(1).

(f)
Not true. Follows from (d) and/or (e).
```
## <span id="18">18</span> 
```C++
(a)
_________________________________________________________________________________________
Statement                                            s/e     Frequency        Total steps
_________________________________________________________________________________________
int factorial(int n)                                   0             0           Theta(0)
{                                                      0             0           Theta(0)
   if (n <= 1) return 1;                               1             1           Theta(1)
   else return n * factorial(n - 1);   1 + tfactorial(n-1)             1   1 + tfactorial(n-1)
}                                                      0             0           Theta(0)
_________________________________________________________________________________________


So, tfactorial(n) = c for n <= 1 and 1 + tfactorial(n-1) for n > 1 (here c is a constant). Using repeated substitution, we get:
tfactorial(n) = 1 + tfactorial(n-1)


            = 2 + tfactorial(n-2)


            = 3 + tfactorial(n-3)


            .


            .


            .


            = n - 1 + tfactorial(1)


            = n - 1 + c


            = Theta(n)




(c) We shall do the analysis for the case n >= 1.
_______________________________________________________________________________________
Statement                                         s/e        Frequency      Total steps
_______________________________________________________________________________________
bool minmax(...)                                    0                0         Theta(0)
{                                                   0                0         Theta(0)
   if (n < 1) return false;                         1                1         Theta(1)
   indexOfMin = indexOfMax = 0;                     1                1         Theta(1)
   for (int i = 1; i < n; i++)                      1         Theta(n)         Theta(n)
      if (a[indexOfMin] > a[i]) indexOfMin = i;     1         Theta(n)         Theta(n)
      else if (a[indexOfMax] ...) indexOfMax = i;   1   Omega(0), O(n)   Omega(0), O(n)
   return true;                                     1                1         Theta(1)
}                                                   0                0         Theta(0)
_______________________________________________________________________________________


So, tminmax(n) = Theta(n), n >= 1.


(f)
_______________________________________________________________________________
Statement                              s/e        Frequency        Total steps
_______________________________________________________________________________
void matrixMultiply(...)                 0                0           Theta(0)
{                                        0                0           Theta(0)
   for (int i = 0; i < m; i++)           1         Theta(m)           Theta(m)
      for (int j = 0; j < p; j++)        1        Theta(mp)          Theta(mp)
      {                                  0                0           Theta(0)
         T sum = 0;                      1        Theta(mp)          Theta(mp)
         for (int k = 0; k < n; k++)     1       Theta(mnp)         Theta(mnp)
            sum += a[i][k] * b[k][j];    1       Theta(mnp)         Theta(mnp)
         c[i][j] = sum;                  1        Theta(mp)          Theta(mp)
      }                                  0                0           Theta(0)
}                                        0                0           Theta(0)
_______________________________________________________________________________


So, tmultiply(m, n, p) = Theta(mnp)


(h) Assume that n >= 1.
___________________________________________________________________________________
Statement                                     s/e   Frequency           Total steps
___________________________________________________________________________________
T polyEval(...)                                 0            0             Theta(0)
{                                               0            0             Theta(0)

   T y = 1, ...;                                1            1             Theta(1)

   for (int i = 1; i <= n; i++)                 1     Theta(n)             Theta(n)
   {                                            0            0             Theta(0)
      y *= x;                                   1     Theta(n)             Theta(n)
      value += y * coeff[i];                    1      Theta(n)            Theta(n)
   }                                            0             0            Theta(0)
   return value;                                1             1            Theta(1)
}                                               0             0            Theta(0)
___________________________________________________________________________________


So, tpolyEval (n) = Theta(n), n >= 1.


(j)
__________________________________________________________________________________________
Statement                                          s/e       Frequency         Total steps
__________________________________________________________________________________________
void rank(...)                                       0               0             Theta(0)
{                                                    0               0             Theta(0)
   for (int i = 0; i < n; i++)                       1         Theta(n)            Theta(n)
      r[i] = 0;                                      1         Theta(n)            Theta(n)

   for (i = 1; i < n; i++)                           1         Theta(n)            Theta(n)
      for (int j = 0; j < i; j++)                    1         Theta(n2)           Theta(n2)
         if (a[j] <= a[i])) r[i]++;                  1         Theta(n2)           Theta(n2)
         else r[j]++;                                1   Omega(0), O(n2)     Omega(0), O(n2)
}                                                    0                0            Theta(0)
__________________________________________________________________________________________


So, trank (n) = Theta(n2).


(l)
________________________________________________________________________________
Statement                                       s/e      Frequency   Total steps
________________________________________________________________________________
void selectionSort(...)                           0              0      Theta(0)
{                                                 0              0      Theta(0)
   for (int size = n; size > 1; size--)           1       Theta(n)      Theta(n)
   {                                              0              0      Theta(0)
      int j = indexOfMax(a, size);      Theta(size)       Theta(n)      Theta(n2)
      swap(a[j], a[size - 1]);                    1       Theta(n)      Theta(n)
   }                                              0              0      Theta(0)
}                                                 0              0      Theta(0)
________________________________________________________________________________


So, tselectionSort (n) = Theta(n2)


(n) First, we obtain the asymptotic complexity of insert.
_________________________________________________________________________________
Statement                                 s/e          Frequency      Total steps
_________________________________________________________________________________
void insert(...)                            0                  0         Theta(0)
{                                           0                  0         Theta(0)
   int i;                                   0                  0         Theta(0)
   for (i = n - 1; i >= 0 && ...)           1     Omega(1), O(n)   Omega(1), O(n)
      a[i+1] = a[i];                        1     Omega(1), O(n)   Omega(1), O(n)

   a[i+1] = x;                              1                  1         Theta(1)
}                                           0                  0         Theta(0)
_________________________________________________________________________________


So, tinsert(n) = Omega(1), O(n)


Now, we analyze the function insertionSort.
____________________________________________________________________________________
Statement                                 s/e           Frequency        Total steps
____________________________________________________________________________________
void insertionSort(...)                      0                   0          Theta(0)
{                                            0                   0          Theta(0)
   for (int i = 1; i < n; i++)               1            Theta(n)          Theta(n)
   {                                         0                   0          Theta(0)
      T t = a[i];                            1            Theta(n)          Theta(n)
      insert(a, i, t);          Omega(1), O(i)            Theta(n)   Omega(n), O(n2)
   }                                         0                   0          Theta(0)
}                                            0                   0          Theta(0)
____________________________________________________________________________________


So, tinsertionSort (n) = Omega(n), O(n2)


(p) First, we obtain the asymptotic complexity of bubble.
_______________________________________________________________________________
Statement                              s/e        Frequency         Total steps
_______________________________________________________________________________
void bubble(...)                         0                0            Theta(0)
{                                        0                0            Theta(0)
   for (int i = 0; i < n - 1; i++)       1         Theta(n)            Theta(n)
      if (a[i].greaterThan(a[i+1]))      1         Theta(n)            Theta(n)
         swap(a[i], a[i + 1]);           1   Omega(0), O(n)      Omega(0), O(n)
}                                        0                0            Theta(0)
_______________________________________________________________________________


So, tbubble (n) = Theta(n)


Now, we analyze the function bubbleSort.
_______________________________________________________________________________
Statement                                    s/e       Frequency    Total steps
_______________________________________________________________________________
_
void bubbleSort(...)                           0               0       Theta(0)
{                                              0               0       Theta(0)
   for (int i = n; i > 1; i--)                 1        Theta(n)       Theta(n)
      bubble(a, i);                     Theta(i)        Theta(n)       Theta(n2)
}                                              0               0       Theta(0)
_______________________________________________________________________________


So, tbubbleSort (n) = Theta(n2)
```
## <span id="19">19</span>
```C++
(a)
Program A is faster than program B when 1000n < 10n2, that is when n > 100.

(b)
Program A is faster than program B when 2n2 < n3, that is when n > 2.

(c)
Program A is faster than program B when 2n < 100n, that is when n < 10.

(d)
Program A is faster than program B when 1000n log2n < n2, that is when n > 1000 log2n. The switchover point is between 213 and 214.
```

## <span id="21">21</span>
```C++
For tA(n) = n, the table entries are xN = 10N, 100N, 1000N, and 1000000N.

For tA(n) = n2, the table entries are sqrt(x)N, for tA(n) = n3, the table entries are x1/3N, and for tA(n) = n5, the table entries are x1/5N.

For tA(n) = 2n, the table entries are log2x N,
```
官方：[https://www.cise.ufl.edu/~sahni/dsaac/chapter3.htm]