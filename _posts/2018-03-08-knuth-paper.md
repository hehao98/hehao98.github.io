---
title: '"Mathematical Analysis of Algorithms" 阅读心得'
date: 2018-03-08
permalink: /posts/2018/03/knuth-paper/
tags:
  - Chinese
  - Math
  - Algorithm
---

原文首发于https://www.cnblogs.com/hehao98/p/8528206.html，如果公式显示不正常请参考原网页。

“Mathematical Analysis of Algorithms”是著名计算机界大神Knuth在1971年发表的论文。以前只是听说Knuth非常神，看了这篇论文才体会到Knuth到底有多神…Orz

此外，特别感谢 @solaaaaa 聚聚，没有他的指导我可能根本看不懂这篇论文…...

## 这篇文章要解决什么问题？

作为算法分析这一领域的早期论文，这篇文章回答了以下两个问题：

1. 算法分析的核心目的是什么？

   使用量化方法来衡量算法的“好坏”。

2. 算法分析解决的是哪些类型的问题？

   A. 对一个特定算法的时间复杂度和空间复杂度的分析。

   B. 对解决一类问题的所有算法进行分析，试图找出“最好”的算法。

此外，本文特别指出，虽然B类的问题看上去比A类的问题更有价值去解决，但对(2)类问题的研究存在两个重大的问题：1、只要对“最好”的定义稍有改变，一个B类问题就会变成另一个完全不同的(2)类问题；2、B类问题往往过于复杂，难以进行有效的数学建模，而如果建立过于简化的模型，容易得到不合常理的结果。出于以上原因，只有少数B类问题（如基于比较的排序） 能得到有效的解决，绝大多数算法分析依然是对A类问题的研究。

之后本文的核心，就是通过两个例子，来展现算法分析的基本思路。

## 例一：In Situ Permutation

### 1. 问题定义

给定一个一维数组$x_1, x_2, …, x_n$和一个对$1,2,…,n$的排列$p(1),p(2),…,p(n)$，我们需要将一维数组$x$根据函数$p$替换为一维数组$x_{p(1)}, x_{p(2)}, …,x_{p(n)} $，有以下要求：

1. 不能修改存储排列$p(1),p(2),…,p(n)$的空间。
2. 整个算法的空间复杂度必须为$O(1)$。

### 2. 设计算法

对以下算法的设计基于以下一个重要的事实：在任意一个排列$p(1),p(2),…,p(n)$，我们总会存在若干个“环”，这个环形如$p(i_1)=i_2,p(i_2)=i_3,…,p(i_k)=i_1$。学过抽象代数的同学可以对此给出一个严格证明。例如对于一个排列：

$$
(p(1), p(2),…,p(9))=(8,2,7,1,6,9,3,4,5)
$$

通过观察我们发现了以下环：

$$
\begin{cases}
p(1)=8, p(8)=4, p(4)=1 \\
p(2)=2 \\
p(3)=7 ,p(7 )=3 \\
p(5)=6,p(6)=9,p(9)=5
\end{cases}
$$

我们就可以定义这个环中最小的值为这个环的头元素。那么只要我们发现了一个环的头元素$k$，就可以将原来的数组中的$x_k$空出来，将紧随其后的元素$x_{p(k)}$填入，然后$x_{p(k)}$的位置就会被空出来可以填入$x_{p(p(k))}$……最后将头元素$x_k$填入环尾部那个排列对应的$x$数组的位置即可。

对应的伪代码描述如下：

```python
for j = 1 to n: # 外循环
    # 判断 j 是不是环的头元素
    # 从p(j)开始遍历这个环
    k = p(j)    
    # 如果j不是环的头元素，那么就会存在一个环上点k<j
    while k > j: # 循环1 a
        k = p(k)
    if k == j:   # 语块2 b
        # k就是环的头元素
        y = x[j], l = p(k)
        while l != j: # 循环3 c 
            x[k] = x[l], k = l, l = p(k)
        x[k] = y
        # 到这一步为止一个环上的元素全部按照排列置换完毕
```

### 3. 算法分析

对一个特定算法分析（A类问题）而言，最重要的是证明算法的正确性。在正确的基础上，我们讨论它的最好情况复杂度，最坏情况复杂度和平均情况复杂度。对平均情况的分析往往有更重要的意义。但就算法分析而言，一般对平均情况的分析会复杂得多，最后常常归结为某个很难的数学问题。

就这个问题而言，为了便于讨论，我们将内层循环和语句块如上面伪代码注释所示进行标号a,b,。

#### 正确性

事实上，算法的设计过程已经简单说明了这个算法的正确性。要给出一个严谨的证明非常麻烦这里不再赘述。

#### 最好情况与最坏情况

显然，外层循环无论如何都会被执行$n$次，因此我们主要考虑内层$a$和$b$的执行次数。

我们先构造只有一个长$n$的环的情况。令

$$
(p(1), p(2),…,p(n))=(2,3,...,n,1)
$$

那么$a$就进入了最坏情况，这样，对于第$i$个外层循环，$a$循环需要执行$n-i$次，总共执行次数为

$$
\sum_{i=1}^n (n-i) = O(n^2)
$$

巧妙的是，此时刚好是$b$的最好情况！因此$b$只用执行一次，这一次执行的复杂度为$O(n)$。

因此，这个最坏情况的执行时间为$O(n^2)$。

我们再构造有$n$个环的情况。令

$$
(p(1),p(2),...,p(n))=(1,2,...,n)
$$

这时$b$进入了最坏情况，$a$进入了最好情况，类似分析可得这种情况的执行时间为$O(n)$。

#### 平均情况

我们首先对这个问题进行重新建模。依然是对之前举过的排列

$$
(p(1), p(2),…,p(9))=(8,2,7,1,6,9,3,4,5)
$$

我们可以将它的环写成$(5,6,9)(3,7)(2)(1,8,4)$，满足：1、每个环开头是其最小的元素。2、每个环的头元素从大到小递减，那么就可以直接表示成另一个排列$(q(1),q(2),…,q(9))=(5,6,9,3,7,2,1,8,4)$，因为我们只要找到其中的数$q_k$使得$q_k=min\{q_1,q_2,…,q_k\}$，那么这个数就是一个环的头元素，这个环从这个元素开始直到下一个具有相同性质的元素之前为止。比如，由于$3=min\{5,6,9,3\}$，我们就发现了$q(4)=3$是一个环的头元素，这个环是$(3,7)$，因为我们发现了$7$之后的$2$比前面所有数都小，所以$2$就是下一个环的元素了。这样，我们就建立了从一个排列$p$到另一个排列$q$的映射。

我们对$q$这个排列，首先研究$a$循环在平均情况下的执行次数。

对于任意一个$a$循环，它从一个随机的环上的元素开始向后遍历，也就是说，如果外循环中$j=q(i)$，$k$就会一直往后进入$q(i+1),q(i+2),…,$直到找到一个位置$q(i+r)$使得$q(i+r) < q(i)$，或者$q(i)$就是环的头元素。所以，当外循环$j=q(i)$时，就会从$q(i)$到$q(i+r)$执行这么多次。这样我们可以用以下方式来表示循环$a$的执行次数。令

$$
y_{ij} = \begin{cases}
1, if\ q(i) < q(k)\ for\ i < k \le j \\
0, \ otherwise
\end {cases}
$$

那么

$$
a=\sum_{1\le i < j \le n}y_{ij}
$$

对于上面的例子而言第一行只有$y_{12}=y_{13}=1$，因为当外循环中的变量$j=q(1)$时，循环$a$会被执行$2$次，直到遍历回到$q(1)$发现$q(1)$就是头元素为止，由于我们构造$q$的时候让头元素递减，所以如果考虑成因为发现$q(1) < q(4)$而退出，不会对研究循环$a$的执行次数造成影响。同样地对于外循环变量$j=q(2)$的情况，只会往后执行$1$次就会发现$q(2) < q(4)$，因此第二行只有$y_{23} = 1 $。类似分析还能找到 $ y_{45}=y_{78}=y_{79}=1 $。


为什么要定义这么一个$ y_{ij} $呢？因为我们非常容易就可以发现$y_{ij}$的平均值$\bar{y}_{ij}$。这个平均值就是总共$ n! $个排列中$y_{ij}=1$的排列个数。这也就是$ q(i)=min(q(k)\mid i \le k \le j) $的概率，也就是$ {1}/({j-i+1}) $（给K神跪了）因此

$$
\begin{align}
\bar{a} &= \sum_{1\le i < j \le n}\bar{y}_{ij}\\
&= \sum_{1\le i < j \le n}\frac{1}{j-i+1} \ \ {(我们固定i先对j求和，然后对i求和)}\\
&= (\frac{1}{2-1+1}+\frac{1}{3-1+1}+...+\frac{1}{n-1+1}) \\
&+(\frac{1}{3-2+1}+\frac{1}{4-2+1}+...+\frac{1}{n-2+1})+...+(\frac{1}{n-(n-1)+1}) \\
&= \frac{n-1}{2}+\frac{n-2}{3}+...+\frac{1}{n} \\
&= \sum_{2 \le r \le n}\frac{n+1-r}{r} \ \ (令r=j-i+1) \\
&= (n+1)(H_n-1)-(n-1) \\
&= (n+1)H_n - 2n  \\
\end {align}
$$

其中$H_n$是调和级数，使用积分法可以证明

$$
H_n=\sum_{i=1}^{n}\frac{1}{i}=O(logn)
$$

所以我们得到$a$循环的平均执行次数为$O(logn)$。

下面分析$b$的执行次数。显然，环有多少个，$b$就会被进入多少次。这所有次数加起来的循环$c$的执行代价为$O(n)$固定不变。因此我们需要考虑$b$平均会被进入多少次，也就是所有长度为$n$排列中平均有多少个环。在Knuth的TAOCP, 1.2.10中已经对此有过分析，因此原文没有写出。（因为我没有TAOCP有大概也看不懂）所以我们只写一个结论：有$k$个环的排列共有$[n,k]$个，这个$[n,k]$是第一类Stirling数。最后可以得到$b$的平均值刚好是调和级数！（我推了推死活推不出来…）

$$
\bar{b} = H_n = O(logn)
$$

通过以上讨论我们就严格证明了平均情况下这个算法的复杂度是$O(n\log n)$。

原文还有关于$a,b$的方差讨论，由于计算极其繁杂在此就不写了。重要的结论是，它的方差证明了$O(n^2)$的最坏情况是非常罕见的。

#### 算法的改进空间

我们可以通过增加一个变量来避免全部元素移动完成后的不必要的遍历，但这不会改善平均情况和最坏情况的复杂度。但是有一个方法可以将最坏情况复杂度降低到$O(n\log n)$，这个方法的关键是对于外循环遍历到的一个$j$，我们同时搜索$p(j), p^{-1}(j),p(p(j)),p^{-1}(p^{-1}(j)),…$,其中$p^{-1}(j)$是其反函数。这样，我们重新考虑最坏情况，显然就是整个排列只有一个长度为$n$的环，例如排列$(1,2,…,n)$。这样，最坏情况就是我们从$j$开始向环的两边搜索到头元素的时间，再加上j在环前面和环后面的长度分别为$k$和$n-k$的部分都处在最坏情况的时间之和。设最坏情况为$f(n)$，就得到如下递推式：

$$
\begin{cases}
f(n)=\max_{1\le k < n}\{\min\{k, n-k\} + f(k) + f(n-k)\} \\
f(1) = 0
\end{cases}
$$

(内心OS：这种东西TM也能解？！)

K神拒绝回答你的提问并直接把答案甩在了你脸上：

$$
f(n)=\sum_{0 \le n < n}v(k) \ \ (v(k)是k的二进制表示中1的个数) \\
f(2^{a_1}+2^{a_2}+...+2^{a_r})=\frac{1}{2}(a_12^{a_1}+(a_2+2)2^{a_2}+...+(a_r+2r-2)2^{a_r}) \\
其中a_1>a_2>...>a_r
$$

在其他几篇由Bush、Mirsky、Drazin、和Griffith发表的论文里有对其复杂度的详细分析。通过这些分析我们知道了这个解法在最坏情况下的复杂度为$O(n\log n)$。（我的内心已经崩溃了）

## 例二：Selecting the t-th largest

### 1. 问题定义

给定一个数组$a_1,a_2,…,a_n$，试用尽可能小的比较次数找出其中第$t$大的值。

### 2. 设计算法

这个问题相对比较常见一些，甚至曾经出现为数据结构作业题……但是其实这个问题想到算法容易，算法的分析并没有那么容易。首先一个$O(n\log n)$的排序算法总能解决我们的问题，但有没有复杂度更低的方法呢？通过快速排序思路的启发我们可以想到这样一个算法，假如我们对数组$a_i,a_{i+1},…,a_j$搜索，首先调用其中的Partition()方法将数组头元素$a_i$的位置放到一个位置使得他左边的元素都比他小，右边的元素都比他大；然后根据他的位置$k$来缩小我们搜索第$t$大数的范围：如果$k=t$我们就找到了这个元素；$k < t$则对$a_{k+1},…,a_j$搜索；$k t $就对$a_i,…,a_{k-1}$搜索。这是一个标准的分治算法。可以写出以下伪代码：

```python
FindtthNumber(a, i, j, t):
    key = a[i]
    # Partition的实现请参考快速排序相关资料
    # Partition返回的是分割后的数组下标
    # 减去数组开头的位置得到a[k]是a[i]-a[j]里第几大的数
    k = Partition(key, a, i, j) - i + 1 
    if k == t:
        return a[k]
    else if k < t:
        return FindtthNumber(a, k + 1, j, t - k)
    else:
        return FindtthNumber(a, i, k - 1, t)
```

### 3. 分析算法

通过伪代码我们可以看出，影响一个子问题的变量有两个：$n$和$t$，$n$是这个子问题中数组的长度，$t$是这个子问题中我们要找的第$t$大的数。不妨设这个子问题为$C(n, t)$。假设我们的分割到什么位置完全随机，即这个子问题分割找到第$1$大、第$2$大、…、第$n$大的数的个数完全相等，均为$1/n$，我们就能分析得到以下递推方程：

$$
\begin{cases}
C(1,1) = 0\\
C(n, t) = n - 1 + \frac{1}{n}(A(n,t)+B(n,t))\\
\end{cases}\\
\mbox{其中} \\
A(n, t)  = C(n - 1,t-1)+C(n-2,t-2)+...+C(n-t+1,1)\\
B(n,t) = C(t,t)+C(t + 1,t) + ...+C(n-1, t)
$$

显然$A(n,t)$对应于递归函数中$k < t$的情况，$B(n,t)$对应于递归函数中$k > t$的情况。

之后我们任务就是求解这个递推方程了。一般人看到这个递推方程大概就会放弃了吧，然而Knuth发现这个递推方程是可以求解的（跪了跪了）！依然是使用差消迭代法。首先通过观察我们看到

$$
A(n+1,t+1) = A(n,t)+C(n,t)\\
B(n+1,t) = B(n,t)+C(n,t)
$$

这样我们就可以把$C(n+1,t+1), C(n,t+1), C(n,t),C(n-1,t)$按如下方式相减：

$$
(n+1)C(n+1,t+1)-nC(n,t+1)-nC(n,t)+(n-1)C(n-1,t) \\
= (n+1)n - n(n-1) - n(n-1) + (n-1)(n-2)\\ + A(n+1,t+1)-A(n,t+1)-A(n,t)+A(n-1,t) \\
+B(n+1,t+1)-B(n,t+1)-B(n,t)+B(n-1,t) \\
= 2 + C(n,t) - C(n-1,t)+C(n,t+1)-C(n-1,t)
$$

推出来

$$
C(n+1,t+1)-C(n,t+1)-C(n,t)+C(n-1,t)=\frac{2}{n+1}\\
(C(n+1,t+1)-C(n,t))-(C(n,t+1)-C(n-1,t))=\frac{2}{n+1}
$$

之后需要列出边界条件，类似之前的推导

$$
\begin{align}
C(n,1)&=n-1+\frac{1}{n}(C(1,1)+C(2,1)+...+C(n-1,1)) \\
(n+1)C(n+1,1)-nC(n,1)&=(n+1)n-n(n-1)+C(n,1)\\
C(n+1,1)-C(n,1)&=\frac{2n}{n+1}=2-\frac{2}{n+1}\\
C(n,1)&=2n-2H_n\\
\Rightarrow C(n,n)&=2n-2H_n\ \ (对称性)
\end{align}
$$

由上述两式可以计算得到

$$
C(n+1,t+1)-C(n,t)=\frac{2}{n+1}+\frac{2}{n}+...+\frac{2}{t+2}+C(t+1,t+1)-C(t,t)\\
=2(H_{n+1}-H_{t+1})+2-\frac{2}{t+1}
$$

不断迭代

$$
C(n,t)=2\sum_{k=2}^{t}(H_{n-t+k}-H_k+1-\frac{1}{k})+C(n+1-t,1)\\
=2((n+1)H_n-(n+3-t)H_{n+1-t}-(t+2)H_t+n+3)
$$

由于调和级数$H_n=O(\log n)$，我们就严格证明了无论$n,t$取什么值，平均情况下算法的复杂度$C(n,t)=O(n)$。我们的算法比较次数已经足够小了，那么如何寻找最少的比较次数？这就从一个A类问题变成了B类问题，并且非常难，感兴趣的读者可以参考相关论文了解对这方面的进展。

## 总结

被前面两个算法搞晕了之后，相信大家已经了解算法分析是个什么样的过程了（笑）。最后Knuth对算法分析做了如下总结：

1. 算法分析对计算机科学领域十分重要
2. 算法分析与离散数学密切相关
3. 算法分析正在形成科学方法
4. 算法分析领域还有很多问题没有解决

## 参考文献

[1] "Mathematical Analysis of Algorithms" Donald Knuth, 1971.