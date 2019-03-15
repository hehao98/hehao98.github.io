---
title: '递推方程的求解'
date: 2018-03-06
permalink: /posts/2018/03/blogpost/recurrence-formula/
tags:
  - Chinese
  - Math
  - Algorithm
---

## 什么是递推方程？

对于序列$a_0,a_1,a_2, …,a_n$，简记为${a_n }$，一个把$a_n$与若干个$a_i (i<n)$联系在一起的等式叫做关于序列${a_n}$的递推方程。

## 为什么要学习求解递推方程？

因为对递归算法的分析离不开递推方程的求解

例如，Hanoi塔问题递归算法为：

```python
Hanoi(A, C, n):                # 将A柱上的n个盘子按照要求移到C柱上
    if n == 1:                 # 只有一个盘子就直接移到C柱s上
        Move(A, C)
    else:                      
        Hanoi(A, B, n – 1)     # 否则先把上面n-1个盘子移到B柱上
        Move(A, C)             # 再把最下面的盘子移到C柱上
        Hanoi(B, C, n – 1)     # 再把那n-1个盘子移到C柱上
```

分析可得递推方程为

$$
\begin{cases} 
T(n) = 2T(n-1) + 1\\ 
T(1) = 1 
\end{cases}
\Rightarrow T(n) = 2^n - 1
$$

## 有哪些求解方法？

1. 迭代法 

    直接迭代：直接将递推式逐层迭代展开，找到求和式规律求解。

    换元迭代：直接迭代展开不方便时，换元成便于直接迭代展开的形式再求解。但这样往往需要对结果进行验证。

    差消迭代：当递推式较为复杂，关联的前项较多时，可以通过将临近递推式适当变形并相减来化成可以迭代求解的形式。

    迭代模型：递归树是对迭代法的直观描述

2. 尝试法：    没有办法的办法

3. 主定理：    是对一类可以迭代求解的递推方程的总结 

## 直接迭代法举例：插入排序最坏情况的复杂度？

插入排序伪代码描述：

```python
# 给定n个数的数组A，输出排序好的数组A 
InsertionSort(A, n):     
    for j = 2 to n:        
        x = A[j]        
        i = j - 1        
        while i > 0 and x < A[j]:
            A[i + 1] = A[i]
            i = i – 1
        A[i + 1] = x
```

最坏情况下，在总共的$n$次迭代中，每次都需要和前面的$n-1$个元素进行比较才能确定插入的位置，那么对于$n$个元素，总的比较次数为前面$n-1$个元素的比较次数再加上自己的$n-1$次比较次数，即得递推方程

$$
\begin{cases}
T(n) = T(n-1)  + n - 1 \\
T(1) = 0
\end{cases}
$$

这样的递推方程解法非常直观，直接逐次迭代，找到和式规律来求解即可。

$$
\begin{align}
T(n)  &= T(n - 1) + n - 1 \\
&= T(n-2)+n-2+n-1 \\
&=... \\
&= T(1) + \sum_{i=1}^{n-1}i \\
&= n(n-1)/2
\end{align}
$$

这样我们就得到了插入排序最坏情况下的复杂度为$O(n^2)$。

## 换元迭代法举例：二分归并排序最坏情况的复杂度？

二分归并排序伪代码描述：

```python
# 对于给定的数组A，将A[p]-A[r]范围内的数排好序
MergeSort(A, p, r):
    if p < r:
        q = (p + r) / 2
        Mergesort(A, p, q);
        MergeSort(A, q + 1, r)
        Merge(A, p, q, r)

# 将按照递增顺序排列好的A[p...q]和A[q+1...r]，输出排序好的数组A[p...r]
Merge(A, p, q, r):
    x = q - p + 1, y = r - q
    将A[p...q]复制到B[1...x], 将A[q+1...r]复制到C[1...y]
    i = 1, j = 1, k = p
    while i <= x and j <= y:
        if B[i] <= C[j]:
            A[k] = B[i]
            i = i + 1
        else:
            A[k] = C[j]
            j = j + 1
        k = k + 1
    if i > x:
        将C[j...y]复制到A[k...r]
    else:
        将B[i...y]复制到A[k...r]

```

对于归并排序的算法分析中，如果假设输入规模$n=2^k$，就可以比较容易地进行分析。

上述算法对于$n=2^k$的数组，两次递归调用分别对$n=2^{k-1}$规模的子问题求解，最后的归并操作，在最坏情况下需要$n-1$次比较运算，则可得递推方程为

$$
\begin{cases}
T(n) = 2T(n/2) + n - 1 \\
T(1) = 0
\end{cases}
$$

对于这样的递推方程，为了便于使用迭代法求解，不妨先设$n=2^k$，当然，这样设相当于我们求的只是递推方程在一部分$n$值下的解，因此在求出结果后应当带入原递推方程验证结果。这种先换元成一种容易求解的形式再迭代求解的方法称为换元迭代法。

$$
\begin{align}
T(2^k) &= 2T(2^{k-1}) + 2^k - 1 \\
&= 2(T(2^{k-2})  +2^{k-1} - 1) + 2^k - 1 \\
&= 4T(2^{k-2})+ 2*2^k - 2 - 1 \\
&= ... \\
&= 2^kT(1) + k2^k - \sum_{i=0}^{k-1}2^i \\
&= k2^k - 2^k + 1 \\
&= n\log n - n + 1
\end{align}
$$

将其带入原来的递推方程可得

$$
\begin{cases}
T(1) = 1log1 - 1 + 1 = 0 \\
2T(n/2) + n - 1 = nlog(n/2) - n + 2 + n - 1 = nlogn - n + 1 = T(n)
\end{cases}
$$

从而验证了我们的解是满足原来的递推方程的。

这样通过以上的分析就证明了二分归并排序在最坏情况下的复杂度为$O(nlogn)$。

## 差消迭代法举例：对快速排序平均情况复杂度的分析

```python
# 将A[p...r]排序
QuickSort(A, p, r):
    if p < r:
        q = Partition(A, p, r)    # 划分数组找到首元素A[p]在排好序后的位置q
        swap(A[p], A[q])
        QuickSort(A, p, q - 1)
        QuickSort(A, q + 1, r)
        
# 对于数组A[p...r]，将A[p]放到适当的位置i使得A[p...i-1]都小于A[i], A[i+1...r]都大于A[i]
Partition(A, p, r):
    x = A[p]
    i = p
    j = r
    while i < j:
        while A[j] >= x:
            j = j - 1
        if i >= j:
            break
        else:
            A[i] = A[j]
            i = i + 1
        while A[i] <= x:
            i = i + 1
        if i >= j:
            break
        else:
            A[j] = A[i]
            j = j - 1
    A[i] = x
    return i
           
```

我们目前只考虑平均情况的分析，假设数组$A$的首元素在排好序后处在$n$个位置中的任何位置都是可能的，即它处在任何位置的概率都是$1/n$，如果它处在位置$i(i=1,2,..,n)$那么两个子问题的规模分别为$i-1$和$n-i$. 考虑到$T(0)=0$，$T(1) = 0$，因此可以得到

$$
\begin{align}
T(n) & = \frac{1}{n}\{[T(0) + T(n-1) ] + [T(1) + T(n-2)] + ... + [T(n-1) + T(0)]\} + O(n) \\
&= \frac{2}{n}\sum_{i=1}^{n-1}T(i) + O(n)
\end{align}
$$

此外，由Partition()算法，可以看到比较次数最坏情况下为$n-1$，因此，不妨设最后一项为$n-1$，从而得到如下递推公式

$$
\begin{cases}
T(n) = \frac{2}{n}\sum_{i=1}^{n-1}T(i) + n-1 \\
T(1) = 0
\end{cases}
$$

当递推式较为复杂，关联的前项较多时，可以通过将临近递推式适当变形并相减来化成可以迭代求解的形式。因此发现可以稍作变形得到

$$
nT(n) = 2\sum_{i-1}^{n-1}T(i) + n^2 - n \\
(n-1)T(n-1) = 2\sum_{i =1}^{n-2}T(i) + (n-1)^2 - (n-1)
$$

将两个方程相减得到（这样求和符号就被消掉了）

$$
nT(n) - (n-1)T(n-1) = 2T(n-1)+2n-2
$$

化简得到

$$
nT(n)=(n+1)T(n-1) + 2n-2
$$

再次变形

$$
\begin{align}
\frac{T(n)}{n+1} &= \frac{T(n-1)}{n} + \frac{2n-2}{n(n+1)} \\
&= \frac{T(n-1)}{n} + \frac{2}{n+1} - \frac{2}{n(n+1)} \\ 
&= ... \\
&=2\sum_{i=3}^{n+1}\frac{1}{i} + \frac{T(1)}{2} + O(\frac{1}{n}) \\
\end{align} \\
\because \sum_{i=3}^{n+1}\frac{1}{i} = \Theta(\log n)(可用积分证明) \therefore T(n) = O(n\log n)
$$

## 迭代模型：递归树

递归树是一种对上述迭代求解的思想的直观描述。

比如对于二分归并排序的方程求解过程就可以画成递归树

又例如：对于以下递推方程

$$
T(n) = T(n/3) + T(2n/3) + n
$$

​             n

​       n/3 2n/3               n

n/9 2n/9 2n/9 4n/9    n

可得这样的递归树，最右边的路径就是最长的路径，这路径共有$\log_{3/2}n$层，每层复杂度都为$O(n)$，易得整个递推方程的复杂度为$O(nlogn)$。

## 尝试法：对快速排序递推方程的求解

之前我们得到过形式为这样的快速排序递推方程，将$O(n)$设为$n-1$以便用迭代法求解

$$
T(n)= \frac{2}{n}\sum_{i=1}^{n-1}T(i) + O(n)
$$

那如果直接对这种形式求解呢？一种没有办法的办法就是估计复杂度带入两边尝试。

1. 如果$T(n)=cn$，右边$=\frac{2}{n}\sum_{i=1}^{n-1}ci + O(n) = cn - c + O(n)$

   两边虽然最高项都是一次项，但是右边一次项的系数更大（因为$O(n)$中还有一次项系数），不成立。

2. 如果$T(n) = cn^2 $，

   $$
\begin{align}
{右边}&=\frac{2}{n}\sum_{i=1}^{n-1}ci^2 + O(n) \\
&= \frac{2c}{n}(\frac{n^3}{3} + O(n^2)) + O(n) \ \ \ \ 
\because  \sum_{i=1}^{n-1}((i+1)^3-i^3))=n^3-1=3\sum_{i=1}^{n-1}i^2+3\sum_{i=1}^{n-1}i+n-1) \\
&= \frac{2c}{3}n^2 + O(n) \ne {左边}
\end{align}
   $$

3. 如果$T(n) = cn\log n$，

   $$
   \begin{align}
   {右边} &= \frac{2c}{n}\sum_{i=1}^{n-1}i\log i + O(n) \\
   & =\frac{2c}{n}[\frac{n^2}{2}\log n - \frac{n^2}{4\ln 2} + O(1)] + O(n) \ \ \ \ ({积分法可证}) \\
   & =cn\log n + O(n)
   \end{align}
   $$
   
   这时左边和右边的最高次项系数相同，因此$T(n)=O(n\log n)$。

## 主定理：总结了一类可以迭代求解的递推方程

设$a\ge 1,b>1$为常数，$f(n)$为函数，$T(n)$为非负整数，且

$$
T(n) = aT(n/b) + f(n)
$$

则有以下结果：

(1) 若$f(n) = O(n^{\log_ba-\varepsilon}),\varepsilon>0$，那么$T(n) = \Theta(n^{\log_ba})$

(2) 若$f(n)=\Theta(n^{\log_ba})$，那么$T(n) = \Theta(n^{\log_ba}\log n)$

(3) 若$f(n) = \Omega(n^{log_ba+\varepsilon}),\varepsilon>0$，且对于某个常数$c<1$和所有充分大的$n$有$af(n/b)\le cf(n)$，那么$T(n)=\Theta(f(n))$.

证明的要点：设$n=b^k$利用迭代法推导即可。情况(3)必须使用附加条件才能推出结果。

### 需要注意的要点：

(1)(3)中的$\varepsilon$，事实上是为了使得$f(n)$的阶严格大或者严格小。

情况(3)中的附加条件需要额外注意。

### 使用主定理的例子

归并排序中的递推式：

$$
\begin{cases}
T(n) = 2T(n/2) + n - 1 \\
T(1) = 0
\end{cases}
$$

属于主定理情况(2)，使用主定理直接得$ T(n)=O(n^{\log_22}\log n)=O(n\log n)$.

### 不能使用主定理的例子

$$
\begin{cases}
T(n) = 2T(n/2) + n\log n \\
T(1) = 1
\end{cases}
$$

根据主定理，$a=b=2$，$f(n)=n\log n$，但是找不到$\varepsilon$使得$f(n)=\Omega(n^{1+\varepsilon})$成立。

使用递归树的方法可以求解得结果等于$T(n) = \Omega(n\log^2 n)$

## 递推方程中$\lfloor x \rfloor$和$\lceil x \rceil$的处理

现猜想解，然后用数学归纳法证明

例如对于以下递推关系：

$$
\begin{cases}
T(n)= 2T(\lfloor \frac{n}{2} \rfloor) + n \\
T(1) = 1
\end{cases}
$$

若没有取整符号，根据主定理即得其阶为$O(n\log n)$

因此猜想$T(n)=O(n\log n)$，下面证明$T(n)\le cn\log n$：

这里使用数学归纳法。

对于$T(1)=1, T(1) <c\ 1 \log 1$不成立

对于$T(2)=2T(\lfloor 1 \rfloor) + 2 = 4 \le 2* 2\log 2$

假设对于小于$n$的正整数命题为真，那么

$$
\begin{align}
T(n)&=2T(\lfloor \frac{n}{2} \rfloor) + n  \\
&\le 2c\lfloor \frac{n}{2} \rfloor log(\lfloor \frac{n}{2} \rfloor) + n \\
&\le 2c\frac{n}{2}(\log n - \log 2) + n \\
&= cn\log n - cn + n \\
&\le cn\log n, \ c = 2
\end{align}
$$

证毕。

