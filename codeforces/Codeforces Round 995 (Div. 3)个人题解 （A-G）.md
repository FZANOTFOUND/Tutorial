# Codeforces Round 995 (Div. 3)个人题解 （A-G）

**所有翻译均为机翻！**
## A.Preparing for the Olympiad

[2051A](https://codeforces.com/contest/2051/problem/A)


**time limit per test: 2 second**

**memory limit per test: 256 megabytes**

### 原题
Monocarp and Stereocarp are preparing for the Olympiad. There are $n$ days left until the Olympiad. On the $i$\-th day, if Monocarp plans to practice, he will solve $a_i$ problems. Similarly, if Stereocarp plans to practice on the same day, he will solve $b_i$ problems.

Monocarp can train on any day he wants. However, Stereocarp watches Monocarp and follows a different schedule: if Monocarp trained on day $i$ and $i < n$, then Stereocarp will train on day $(i+1)$.

Monocarp wants to organize his training process in a way that the difference between the number of problems he solves and the number of problems Stereocarp solves is as large as possible. Formally, Monocarp wants to maximize the value of $(m-s)$, where $m$ is the number of problems he solves, and $s$ is the number of problems Stereocarp solves. Help Monocarp determine the maximum possible difference in the number of solved problems between them.

Monocarp 和 Stereocarp 正在为奥林匹克竞赛做准备。离奥林匹克竞赛还有 $n$ 天。在第 $i$ 天，如果Monocarp计划练习，他将解决 $a_i$ 个问题。同样，如果Stereocarp计划在同一天练习，他将解决 $b_i$ 个问题。

单卡可以在任何一天进行训练。然而，Stereocarp会观察 Monocarp，并遵循不同的时间表：如果 Monocarp 在 $i$ ( $i < n$) 天进行了训练，那么Stereocarp将在 $(i+1)$ 天进行训练。

Monocarp 希望在组织训练过程时，他所解决的问题数量与 Stereocarp 所解决的问题数量之间的差距越大越好。从形式上看，Monocarp希望最大化 $(m-s)$ 的值，其中 $m$ 是他解决的问题数，而 $s$ 是立Stereocarp解决的问题数。帮助 Monocarp 确定他们之间已解决问题数的最大可能差异。

**Input**

The first line contains a single integer $t$ ($1 \le t \le 10^3$) — the number of test cases.

The first line of each test case contains a single integer $n$ ($1 \le n \le 100$).

The second line contains $n$ integers $a_1, a_2, \dots, a_n$ ($1 \le a_i \le 100$).

The third line contains $n$ integers $b_1, b_2, \dots, b_n$ ($1 \le b_i \le 100$).

第一行包含一个整数 $t$ ( $1 \le t \le 10^3$ ) - 测试用例数。

每个测试用例的第一行包含一个整数 $n$ ( $1 \le n \le 100$ )。

第二行包含 $n$ 个整数 $a_1, a_2, \dots, a_n$ ( $1 \le a_i \le 100$ )。

第三行包含 $n$ 个整数 $b_1, b_2, \dots, b_n$ ( $1 \le b_i \le 100$ )。


**Output**

For each test case, print a single integer — the maximum possible difference between the number of problems Monocarp solves and the number of problems Stereocarp solves.

对于每个测试用例，打印一个整数 - Monocarp 解决的问题数与 Stereocarp 解决的问题数之间可能存在的最大差异。


**Example**

Input

4
2
3 2
2 1
1
5
8
3
1 1 1
2 2 2
6
8 2 5 6 2 6
8 2 7 4 3 4

Output

4
5
1
16

**Note**

Let's analyze the example from the statement:

-   In the first test case, it is optimal for Monocarp to train both days; then Stereocarp will train on day $2$.
-   In the second test case, it is optimal for Monocarp to train on the only day, and Stereocarp will not train at all.
-   In the third test case, it is optimal for Monocarp to train on the last day (and only on that day).
-   In the fourth test case, it is optimal for Monocarp to train on days $1, 3, 4, 6$; then Stereocarp will train on days $2, 4, 5$.

让我们分析一下声明中的例子：

- 在第一个测试案例中，最理想的情况是 Monocarp 两天都进行训练；然后 Stereocarp 在 $2$ 天进行训练。
- 在第二个测试案例中，最佳方案是 Monocarp 在唯一的一天进行训练，而 Stereocarp 完全不训练。
- 在第三个测试用例中，Monocarp 在最后一天（而且只在这一天）进行训练是最佳选择。
- 在第四个测试案例中，Monocarp 在 $1, 3, 4, 6$ 天进行训练是最佳选择；然后 Stereocarp 将在 $2, 4, 5$ 天进行训练。

### 题解
为了最大化差异，Monocarp应当只在$a_{i} > b_{i+1}$时进行训练。同时Monocarp在第$n$天训练
时，Stereocarp无法跟着在下一天进行训练。

代码如下

```python
t = int(input())
for _ in range(t):
    n = int(input()) 
    a = list(map(int, input().split()))
    b = list(map(int, input().split()))
    ans = 0
    for i in range(n-1):
        if a[i] > b[i+1]:
            ans += a[i] - b[i+1]
    ans += a[-1]
    print(ans)
```

## B.Journey

[2051B](https://codeforces.com/contest/2051/problem/B)

**time limit per test: 1 second**

**memory limit per test: 256 megabytes**

### 原题

Monocarp decided to embark on a long hiking journey.

He decided that on the first day he would walk $a$ kilometers, on the second day he would walk $b$ kilometers, on the third day he would walk $c$ kilometers, on the fourth day, just like on the first, he would walk $a$ kilometers, on the fifth day, just like on the second, he would walk $b$ kilometers, on the sixth day, just like on the third, he would walk $c$ kilometers, and so on.

Monocarp will complete his journey on the day when he has walked at least $n$ kilometers in total. Your task is to determine the day on which Monocarp will complete his journey.


Monocarp 决定开始一次长途徒步旅行。

他决定第一天走 $a$ 公里，第二天走 $b$ 公里，第三天走 $c$ 公里，第四天和第一天一样，走 $a$ 公里，第五天和第二天一样，走 $b$ 公里，第六天和第三天一样，走 $c$ 公里，以此类推。

当Monocarp总共走了至少 $n$ 千米时，他就完成了他的旅程。你的任务是确定 Monocarp 将在哪一天完成他的旅程。


**Input**

The first line contains one integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

Each test case consists of one line containing four integers $n$, $a$, $b$, $c$ ($1 \le n \le 10^9$; $1 \le a, b, c \le 10^6$).

第一行包含一个整数 $t$ ( $1 \le t \le 10^4$ ) - 测试用例数。

每个测试用例由一行组成，包含四个整数 $n$ , $a$ , $b$ , $c$ ( $1 \le n \le 10^9$ ; $1 \le a, b, c \le 10^6$ )。

**Output**

For each test case, output one integer — the day on which Monocarp will have walked at least $n$ kilometers in total and will complete his journey.

对于每个测试用例，输出一个整数 - Monocarp 将至少走完 $n$ 千米并完成其旅程的那一天。

**Example**

Input

4
12 1 5 3
6 6 7 4
16 3 4 1
1000000000 1 1 1

Output

5
1
6
1000000000

**Note**

In the first example, over the first four days, Monocarp will cover $1 + 5 + 3 + 1 = 10$ kilometers. On the fifth day, he will cover another $5$ kilometers, meaning that in total over five days he will have covered $10 + 5 = 15$ kilometers. Since $n = 12$, Monocarp will complete his journey on the fifth day.

In the second example, Monocarp will cover $6$ kilometers on the first day. Since $n = 6$, Monocarp will complete his journey on the very first day.

In the third example, Monocarp will cover $3 + 4 + 1 + 3 + 4 + 1 = 16$ kilometers over the first six days. Since $n = 16$, Monocarp will complete his journey on the sixth day.

在第一个例子中，前四天，Monocarp将走 $1 + 5 + 3 + 1 = 10$ 公里。第五天，他将再走 $5$ 公里，这意味着五天他总共将走 $10 + 5 = 15$ 公里。自 $n = 12$ 起，Monocarp将在第五天完成他的旅程。

在第二个例子中，Monocarp将在第一天走完 $6$ 千米。由于 $n = 6$ ，Monocarp将在第一天完成他的旅程。

在第三个例子中，Monocarp将在前六天走 $3 + 4 + 1 + 3 + 4 + 1 = 16$ 公里。由于 $n = 16$ ，
Monocarp将在第六天完成旅程。
### 题解
模拟即可

代码如下
```python
t = int(input())
for _ in range(t):
    n, a, b, c = map(int, input().split())
    tt = n//(a+b+c)
    d = tt * 3
    use = (a+b+c) * tt
    if use < n:
        d += 1
        use += a
    if use < n:
        d += 1
        use += b
    if use < n:
        d += 1
        use += c
    print(d)
```

## C.Preparing for the Exam

[2051C](https://codeforces.com/contest/2051/problem/C)

**time limit per test: 1.5 second**

**memory limit per test: 256 megabytes**

### 原题


Monocarp is preparing for his first exam at the university. There are $n$ different questions which can be asked during the exam, numbered from $1$ to $n$. There are $m$ different lists of questions; each list consists of exactly $n-1$ different questions. Each list $i$ is characterized by one integer $a_i$, which is the index of the only question which is **not present** in the $i$\-th list. For example, if $n = 4$ and $a_i = 3$, the $i$\-th list contains questions $[1, 2, 4]$.

During the exam, Monocarp will receive one of these $m$ lists of questions. Then, the professor will make Monocarp answer all questions from the list. So, Monocarp will pass only if he knows all questions from the list.

Monocarp knows the answers for $k$ questions $q_1, q_2, \dots, q_k$. For each list, determine if Monocarp will pass the exam if he receives that list.


Monocarp正在准备他在大学里的第一次考试。在考试中，有 $n$ 个不同的问题，编号从 $1$ 到 $n$ 。有 $m$ 个不同的问题列表；每个列表由恰好 $n-1$ 个不同的问题组成。每个问题列表 $i$ 都有一个整数 $a_i$ ，该整数是 $i$ -列表中唯一**不存在**的问题的索引。例如，如果有 $n = 4$ 和 $a_i = 3$ ，那么 $i$ /th列表就包含问题 $[1, 2, 4]$ 。

在考试期间，Monocarp会收到这些 $m$ 问题列表中的一个。然后，教授会让 Monocarp 回答列表中的所有问题。因此，只有当Monocarp知道列表中的所有问题时，他才能通过考试。

Monocarp 知道 $k$ 个问题的答案 $q_1, q_2, \dots, q_k$ 。对于每份清单，请判断如果Monocarp收到该清单，他是否能通过考试。


**Input**


The first line contains one integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

Each test case consists of three lines:

-   the first line contains three integers $n$, $m$ and $k$ ($2 \le n \le 3 \cdot 10^5$; $1 \le m, k \le n$);
-   the second line contains $m$ **distinct** integers $a_1, a_2, \dots, a_m$ ($1 \le a_i \le n$; $a_i < a_{i+1}$);
-   the third line contains $k$ **distinct** integers $q_1, q_2, \dots, q_k$ ($1 \le q_i \le n$; $q_i < q_{i+1}$).

Additional constraints on the input:

-   the sum of $n$ over all test cases does not exceed $3 \cdot 10^5$.


第一行包含一个整数 $t$ ( $1 \le t \le 10^4$ ) - 测试用例数。

每个测试用例由三行组成：

- 第一行包含三个整数 $n$ 、 $m$ 和 $k$ ( $2 \le n \le 3 \cdot 10^5$ ; $1 \le m, k \le n$ )；
- 第二行包含 $m$ 个整数**不同**的整数 $a_1, a_2, \dots, a_m$ （ $1 \le a_i \le n$ ； $a_i < a_{i+1}$ ）；
- 第三行包含 $k$ **distinct** 整数 $q_1, q_2, \dots, q_k$ ( $1 \le q_i \le n$ ; $q_i < q_{i+1}$ )。

输入的其他限制：

- 所有测试用例中 $n$ 的总和不超过 $3 \cdot 10^5$ 。


**Output**

For each test case, print a string of $m$ characters. The $i$\-th character should be 1 if Monocarp passes the exam if he receives the $i$\-th question list, 0 if Monocarp won't pass.

对于每个测试用例，打印一个由 $m$ 个字符组成的字符串。如果 Monocarp 收到 $i$ -问题列表就能通过考试，那么 $i$ -字符应为 1；如果 Monocarp 不能通过考试，那么 $i$ -字符应为 0。

**Example**

Input

4
4 4 3
1 2 3 4
1 3 4
5 4 3
1 2 3 4
1 3 4
4 4 4
1 2 3 4
1 2 3 4
2 2 1
1 2
2


Output

0100
0000
1111
10


**Note**

In the first test case, Monocarp knows the questions $[1, 3, 4]$. Let's consider all the question lists:

-   the first list consists of questions $[2, 3, 4]$. Monocarp doesn't know the $2$\-nd question, so he won't pass;
-   the second list consists of questions $[1, 3, 4]$. Monocarp knows all these questions, so he will pass;
-   the third list consists of questions $[1, 2, 4]$. Monocarp doesn't know the $2$\-nd question, so he won't pass;
-   the fourth list consists of questions $[1, 2, 3]$. Monocarp doesn't know the $2$\-nd question, so he won't pass.

在第一个测试案例中，Monocarp 知道问题 $[1, 3, 4]$ 。让我们考虑所有的问题列表：

- 第一个问题列表包含 $[2, 3, 4]$ 个问题。Monocarp 不知道 $2$ \-nd 问题，所以他不会通过；
- 第二张单子由 $[1, 3, 4]$ 个问题组成。莫诺卡普知道所有这些问题，所以他能通过；
- 第三张试卷由 $[1, 2, 4]$ 道题组成。Monocarp 不知道第 $2$ 个问题，所以他不会通过；
- 第四个问题是 $[1, 2, 3]$ 。Monocarp不知道 $2$ nd问题，所以他不会通过。
### 题解

- 由于每张试卷都有$n-1$个问题，因此当Monocarp知道的问题数量没达到$n-1$时，他将无法通过任何一场考试。

- 当Monocarp知道全部的$n$个问题时，他必定能通过所有考试。

- 当Monocarp知道$n-1$个问题时，若题目不包含的题Monocarp恰好不会，则Monocarp能通过这场考试，否则不能。

代码如下

```cpp
#include <bits/stdc++.h>
using namespace std;
      
typedef long long ll;

inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
       
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
       
void print(ll x){pt(x), puts("");}
    
ll know[maxn], a[maxn];
void solve(){
    memset(know, 0, sizeof know);
    ll n = read(), m = read(), k = read();
    for(ll i=0;i<m;i++){
        a[i] = read();
    }
    for(ll i=0;i<k;i++){
        know[read()] = 1;
    }
    if (k<n-1){
        for(ll i=0;i<m;i++){
            putchar('0');
        }
    }
    else if (k==n){
        for(ll i=0;i<m;i++){
            putchar('1');
        }
    }
    else{
        for(ll i=0;i<m;i++){
            if (!know[a[i]]){
                putchar('1');
            }
            else{
                putchar('0');
            }
        }
    }
    puts("");
    
}

int main(){
    ll t = read();
    while (t--){
        solve();
    }
}
```

## D. Counting Pairs

[2051D](https://codeforces.com/contest/2051/problem/D)

**time limit per test: 2 second**

**memory limit per test: 256 megabytes**

### 原题



You are given a sequence $a$, consisting of $n$ integers, where the $i$\-th element of the sequence is equal to $a_i$. You are also given two integers $x$ and $y$ ($x \le y$).

A pair of integers $(i, j)$ is considered interesting if the following conditions are met:

-   $1 \le i < j \le n$;
-   if you simultaneously remove the elements at positions $i$ and $j$ from the sequence $a$, the sum of the remaining elements is at least $x$ and at most $y$.

Your task is to determine the number of interesting pairs of integers for the given sequence $a$.



给你一个由 $n$ 个整数组成的序列 $a$ ，其中序列的 $i$ -th 元素等于 $a_i$ 。同时还给出了两个整数 $x$ 和 $y$ ( $x \le y$ )。

如果满足以下条件，一对整数 $(i, j)$ 就会被认为是有趣的：

- $1 \le i < j \le n$ ;
- 如果同时从序列 $a$ 中删除位置 $i$ 和 $j$ 的元素，则剩余元素的和至少为 $x$ ，最多为 $y$ 。

你的任务是确定给定序列 $a$ 中有趣的整数对的数目。



**Input**

The first line contains one integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

Each test case consists of two lines:

-   The first line contains three integers $n, x, y$ ($3 \le n \le 2 \cdot 10^5$, $1 \le x \le y \le 2 \cdot 10^{14}$);
-   The second line contains $n$ integers $a_1, a_2, \dots, a_n$ ($1 \le a_i \le 10^{9}$).

Additional constraint on the input: the sum of $n$ across all test cases does not exceed $2 \cdot 10^5$.



第一行包含一个整数 $t$ ( $1 \le t \le 10^4$ )—测试用例的数量。

每个测试用例由两行组成：

-第一行包含三个整数 $n, x, y$ ( $3 \le n \le 2 \cdot 10^5$ ，$1 \le x \le y \le 2 \cdot 10^{14}$ )

-第二行包含 $n$ 个整数 $a < 1, a < 2, \dots, a < n$ ( $1 \le a < i \le 10^{9}$ )。

对输入的附加约束：所有测试用例中 $n$ 的总和不超过 $2 \cdot 10^5$ 。



**Output**

For each test case, output one integer — the number of interesting pairs of integers for the given sequence $a$.

对于每个测试用例，输出一个整数 - 给定序列 $a$ 中有趣的整数对的数量。

**Example**

Input

7
4 8 10
4 6 3 6
6 22 27
4 9 6 3 4 5
3 8 10
3 2 1
3 1 1
2 3 4
3 3 6
3 2 1
4 4 12
3 3 2 1
6 8 8
1 1 2 2 2 3



Output

4
7
0
0
1
5
6




**Note**

In the first example, there are $4$ interesting pairs of integers:

1.  $(1, 2)$;
2.  $(1, 4)$;
3.  $(2, 3)$;
4.  $(3, 4)$.

在第一个例子中，有 $4$ 个有趣的整数对：

6.  $(1, 2)$ ;
7.  $(1, 4)$ ;
8.  $(2, 3)$ ;
9.  $(3, 4)$ .
### 题解
令$S = \sum_{i=1}^{n} a_{i}$

$\because x \le S - (a_{i} + a_{j}) \le y$

$\therefore S - a_{i} - y \le a_{j} \le S - a_{i} - x$

先对$a$排序。对每个$a_{i}$，我们可以二分寻找所有满足条件的$a_{j}$，为了不重复计算，每次只加上在$i$右边的$a_{j}$。

代码如下

```python
from bisect import bisect_left, bisect_right
t = int(input())
for _ in range(t):
    n, x, y = map(int, input().split())
    a = list(map(int, input().split()))
    sa = sum(a)
    a.sort()
    ans = 0
    for i in range(n):
        l = max(bisect_left(a, sa - a[i] - y), i+1)
        r = max(bisect_right(a, sa - a[i] - x), i+1)
        if l<r:
            ans += r-l
    print(ans)
```
## E. Best Price

[2051E](https://codeforces.com/contest/2051/problem/E)

**time limit per test: 2 second**

**memory limit per test: 256 megabytes**

### 原题




A batch of Christmas trees has arrived at the largest store in Berland. $n$ customers have already come to the store, wanting to buy them.

Before the sales begin, the store needs to determine the price for one tree (the price is the same for all customers). To do this, the store has some information about each customer.

For the $i$\-th customer, two integers $a_i$ and $b_i$ are known, which define their behavior:

-   if the price of the product is at most $a_i$, the customer will buy a tree and leave a positive review;
-   otherwise, if the price of the product is at most $b_i$, the customer will buy a tree but leave a negative review;
-   otherwise, the customer will not buy a tree at all.

Your task is to calculate the maximum possible earnings for the store, given that it can receive no more than $k$ negative reviews.

一批圣诞树已经抵达伯兰最大的商店。 $n$ 顾客已经来到商店，想要购买它们。在销售开始之前，商店需要确定一棵树的价格(所有客户的价格相同)。

为了做到这一点，商店有一些关于每个客户的信息。对于第 $i$ 个客户，已知两个整数 $a < i$ 和 $b < i$ 。

这定义了他们的行为：

-如果产品的价格最多为 $a < i$ ，

客户将购买一棵树，并留下积极的评论

-否则，如果产品的价格最多为 $b < i$ ，客户将购买一棵树，但留下负面评论

-否则，客户根本不会购买树。您的任务是计算商店的最大可能收入，前提是该商店收到的负面评论不超过 $k$ 条。



**Input**

The first line contains a single integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

The first line of each test case contains two integers $n$ and $k$ ($1 \le n \le 2 \cdot 10^5$; $0 \le k \le n$).

The second line contains $n$ integers $a_1, a_2, \dots, a_n$ ($1 \le a_i \le 2 \cdot 10^9$).

The third line contains $n$ integers $b_1, b_2, \dots, b_n$ ($1 \le b_i \le 2 \cdot 10^9$; $a_i < b_i$).

Additional constraint on the input: the sum of $n$ over all test cases does not exceed $2 \cdot 10^5$.

第一行包含单个整数 $t$ ( $1 \le t \le 10^4$ )—测试用例的数量。

每个测试用例的第一行包含两个整数 $n$ 和 $k$ ( $1 \le n \le 2 \cdot 10^5$ ;$0 \le k \le n$ )。

第二行包含 $n$ 整数 $a _ 1, a _ 2, \dots, a _ n$ ( $1 \le a _ i \le 2 \cdot 10^9$ )。

第三行包含 $n$ 个整数 $b _ 1, b _ 2, \dots, b _ n$ ( $1 \le b _ i \le 2 \cdot 10^9$; $a _ i < b _ i$ )。

对输入的附加约束：所有测试用例的 $n$ 的总和不超过 $2 \cdot 10^5$ 。




**Output**

For each test case, print a single integer — the maximum possible earnings for the store, given that it can receive no more than $k$ negative reviews.


对于每个测试用例，打印一个整数—商店的最大可能收入，假设它可以接收不超过 $k$ 个负面评论。


**Example**

Input

5
2 0
2 1
3 4
1 1
2
5
3 3
1 5 2
3 6 4
4 3
2 3 2 8
3 7 3 9
3 1
2 9 5
12 14 9


Output

2
5
9
14
15


**Note**

Consider the example from the statement:

-   In the first test case, the price should be set to $1$. Then both customers will buy one tree each and leave no negative reviews;
-   In the second test case, the price should be set to $5$. Then the only customer will buy a tree and leave a negative review;
-   In the third test case, the price should be set to $3$. Then all customers will buy one tree each, and the store will receive two negative reviews.
-   In the fourth test case, the price should be set to $7$. Then two customers will buy one tree each, and the store will receive one negative review.

请看声明中的例子：

- 在第一个测试案例中，价格应设置为 $1$ 。那么两位客户将各购买一棵树，并且不会留下负面评论；
- 在第二个测试案例中，价格应设置为 $5$ 。那么唯一的一位顾客会购买一棵树，并留下负面评论；
- 在第三个测试案例中，价格应设置为 $3$ 。那么所有顾客每人都会购买一棵树，商店会收到两条负面评论。
- 在第四个测试案例中，价格应设置为 $7$ 。然后，两名顾客每人购买一棵树，商店将收到一条负面评论。
### 题解
首先，最终商品的价格一定是$a_i$或$b_i$（$1 \le i \le n$），可以反证法证明。

假设价格不是$a_i$或$b_i$，则将价格升高$1$不会改变收到的负面评论的个数，也不会改变购买树的人数。

因此价格一定是$a_i$或$b_i$。

对每个$a_i$或$b_i$，我们二分得到多少人会买，有多少人买了但给差评。如果少于等于$k$个人给差评，更新最大值。

代码如下
```cpp
#include <bits/stdc++.h>
using namespace std;
      
typedef long long ll;

  
inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
       
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
       
void print(ll x){pt(x), puts("");}
    

void solve(){
    ll n = read(), k = read();
    vector<ll> a(n), b(n), v;
    for(ll i=0;i<n;i++){
        a[i] = read();
        v.push_back(a[i]);
    }
    for(ll i=0;i<n;i++){
        b[i] = read();
        v.push_back(b[i]);
    }
    sort(a.begin(), a.end());
    sort(b.begin(), b.end());
    sort(v.begin(), v.end());
    v.erase(unique(v.begin(), v.end()), v.end());
    ll ans = 0;
    for(ll p:v){
        ll n1 = n - (lower_bound(a.begin(), a.end(), p) - a.begin());
        ll n2 = n - (lower_bound(b.begin(), b.end(), p) - b.begin());
        if (n2-n1<=k) ans = max(ans, p*max(n1, n2));
    }
    print(ans);
}

int main(){
    ll t = read();
    while(t--){
        solve();
    }
}
```
## F. Joker

[2051F](https://codeforces.com/contest/2051/problem/F)

**time limit per test: 2 second**

**memory limit per test: 256 megabytes**

### 原题


Consider a deck of $n$ cards. The positions in the deck are numbered from $1$ to $n$ from top to bottom. A joker is located at position $m$.

$q$ operations are applied sequentially to the deck. During the $i$\-th operation, you need to take the card at position $a_i$ and move it either to the beginning or to the end of the deck. For example, if the deck is $[2, 1, 3, 5, 4]$, and $a_i=2$, then after the operation the deck will be either $[1, 2, 3, 5, 4]$ (the card from the second position moved to the beginning) or $[2, 3, 5, 4, 1]$ (the card from the second position moved to the end).

Your task is to calculate the number of distinct positions where the joker can be after each operation.


考虑一副 $n$ 牌。卡片组中的位置从上到下编号为 $1$ 至 $n$ 。小丑位于位置 $m$ 。

$q$ 操作按顺序应用于卡片组。

在第 $i$ 次操作中，您需要拿起位置 $a _ i$ 处的牌，并将其移动到牌组的开头或结尾。例如，如果卡片组是 $[2, 1, 3, 5, 4]$ 和 $a _ i=2$ ，然后在操作之后，这副牌将是 $[1, 2, 3, 5, 4]$ (从第二个位置移动到开始的牌)或 $[2, 3, 5, 4, 1]$ (从第二个位置移动到末尾的卡片)。您的任务是计算每次操作后小丑可以出现的不同位置的数量。



**Input**

The first line contains a single integer $t$ ($1 \le t \le 10^4$) — the number of test cases.

The first line of each test case contains three integers $n$, $m$, and $q$ ($2 \le n \le 10^9$; $1 \le m \le n$; $1 \le q \le 2 \cdot 10^5$).

The second line contains $q$ integers $a_1, a_2, \dots, a_q$ ($1 \le a_i \le n$).

Additional constraint on the input: the sum of $q$ over all test cases does not exceed $2 \cdot 10^5$.


第一行包含单个整数 $t$ ( $1 \le t \le 10^4$ )—测试用例的数量。

每个测试用例的第一行包含三个整数 $n$ 、 $m$ 和 $q$ ( $2 \le n \le 10^9$ $1 \le m \le n$ $1 \le q \le 2 \cdot 10^5$ )。

第二行包含 $q$ 整数 $a _ 1, a _ 2, \dots, a _ q$ ( $1 \le a _ i \le n$ )。

对输入的附加约束：所有测试用例的 $q$ 的总和不超过 $2 \cdot 10^5$ 。

**Output**

For each test case, print $q$ integers — the number of distinct positions where the joker can be after each operation.


对于每个测试用例，打印 $q$ 个整数—每个操作后Joker可以位于的不同位置的数量。

**Example**

Input

5
6 5 3
1 2 3
2 1 4
2 1 1 2
5 3 1
3
3 2 4
2 1 1 1
18 15 4
13 15 1 16

Output

2 3 5 
2 2 2 2 
2 
2 3 3 3 
2 4 6 8 

**Note**

Consider the example from the statement:

-   In the first test case, the price should be set to $1$. Then both customers will buy one tree each and leave no negative reviews;
-   In the second test case, the price should be set to $5$. Then the only customer will buy a tree and leave a negative review;
-   In the third test case, the price should be set to $3$. Then all customers will buy one tree each, and the store will receive two negative reviews.
-   In the fourth test case, the price should be set to $7$. Then two customers will buy one tree each, and the store will receive one negative review.

请看声明中的例子：

- 在第一个测试案例中，价格应设置为 $1$ 。那么两位客户将各购买一棵树，并且不会留下负面评论；
- 在第二个测试案例中，价格应设置为 $5$ 。那么唯一的一位顾客会购买一棵树，并留下负面评论；
- 在第三个测试案例中，价格应设置为 $3$ 。那么所有顾客每人都会购买一棵树，商店会收到两条负面评论。
- 在第四个测试案例中，价格应设置为 $7$ 。然后，两名顾客每人购买一棵树，商店将收到一条负面评论。
### 题解

我们维护$Joker$可能在的位置的区间

对一个区间$[l,r]$考虑三种情况

- $a_i < l$， 此时只有将$a_i$位置的数移动带尾部会产生新位置，即区间向左扩大一位
- $a_i > r$， 此时只有将$a_i$位置的数移动带尾部会产生新位置，即区间向左扩大一位
- $l \le a_i \le r$，此时会产生$[1, 1]$, $[n, n]$两个新区间，区间会成$[l, a_i-1]$和$[a_i+1, r]$两部分。对这两部分来说，如果存在（即长度大于$0$），上面两种情况仍需考虑（剩余的值会扩张）

我们每次判断完后进行区间合并，区间长度的和即为当前的答案。

代码如下
```python
def merge(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = []
    for interval in intervals:
        if not merged or merged[-1][1] < interval[0]:
            merged.append(interval)
        else:
            merged[-1][1] = max(merged[-1][1], interval[1])
    return merged

t = int(input())
for _ in range(t):
    n, m, q = map(int, input().split())
    a = list(map(int, input().split()))
    segs = [[m, m]]
    for p in a:
        split = 0
        for i in range(len(segs)):
            if (segs[i][0] <= p <= segs[i][1]):
                l, r = segs[i]
                segs.pop(i)
                if l+1<=p:
                    segs.append([l, p-1])
                if p <= r-1:
                    segs.append([p+1 , r])
                split = 1
                break
        for i in range(len(segs)):
            if (p < segs[i][0]):
                segs[i][0] -= 1
            if (p > segs[i][1]):
                segs[i][1] += 1
        if split:
            segs += [[1, 1], [n, n]]
        segs = merge(segs)
        ans = 0
        for l, r in segs:
            ans += r-l+1
        print(ans, end = ' ')
    print()

```
AI翻译的C++版本~~（有人用c++写写红温了）~~ 
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// 定义merge函数，用于合并重叠的区间
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b) {
        return a[0] < b[0];
    });
    vector<vector<int>> merged;
    for (const auto& interval : intervals) {
        if (merged.empty() || merged.back()[1] < interval[0]) {
            merged.push_back(interval);
        } else {
            merged.back()[1] = max(merged.back()[1], interval[1]);
        }
    }
    return merged;
}

int main() {
    int t;
    cin >> t;
    for (int _ = 0; _ < t; ++_) {
        int n, m, q;
        cin >> n >> m >> q;
        vector<int> a(q);
        for (int i = 0; i < q; ++i) {
            cin >> a[i];
        }
        vector<vector<int>> segs = {{m, m}};
        for (int p : a) {
            int split = 0;
            for (int i = 0; i < segs.size(); ++i) {
                if (segs[i][0] <= p && p <= segs[i][1]) {
                    int l = segs[i][0], r = segs[i][1];
                    segs.erase(segs.begin() + i);
                    if (l + 1 <= p) {
                        segs.push_back({l, p - 1});
                    }
                    if (p <= r - 1) {
                        segs.push_back({p + 1, r});
                    }
                    split = 1;
                    break;
                }
            }
            for (auto& seg : segs) {
                if (p < seg[0]) {
                    seg[0] -= 1;
                }
                if (p > seg[1]) {
                    seg[1] += 1;
                }
            }
            if (split) {
                segs.push_back({1, 1});
                segs.push_back({n, n});
            }
            segs = merge(segs);
            int ans = 0;
            for (const auto& seg : segs) {
                ans += seg[1] - seg[0] + 1;
            }
            cout << ans << " ";
        }
        cout << endl;
    }
    return 0;
}
```


## G. Snakes

[2051G](https://codeforces.com/contest/2051/problem/G)


**time limit per test: 3 second**

**memory limit per test: 512 megabytes**

### 原题

Suppose you play a game where the game field looks like a strip of $1 \times 10^9$ square cells, numbered from $1$ to $10^9$.

You have $n$ snakes (numbered from $1$ to $n$) you need to place into some cells. Initially, each snake occupies exactly one cell, and you can't place more than one snake into one cell. After that, the game starts.

The game lasts for $q$ seconds. There are two types of events that may happen each second:

-   snake $s_i$ enlarges: if snake $s_i$ occupied cells $[l, r]$, it enlarges to a segment $[l, r + 1]$;
-   snake $s_i$ shrinks: if snake $s_i$ occupied cells $[l, r]$, it shrinks to a segment $[l + 1, r]$.

Each second, exactly one of the events happens.

If at any moment of time, any snake runs into some obstacle (either another snake or the end of the strip), you lose. Otherwise, you win with the score equal to the maximum cell occupied by any snake so far.

What is the minimum possible score you can achieve?


假设您玩一个游戏，其中游戏区域看起来像一条 $1 \times 10^9$ 正方形单元格，编号从 $1$ 到 $10^9$ 。您需要将 $n$ 条蛇(编号从 $1$ 到 $n$ )放置到一些单元格中。

最初，每条蛇正好占据一个细胞，你不能在一个细胞中放置多条蛇。之后，游戏开始。游戏持续 $q$ 秒。

每秒钟可能发生两种类型的事件：

-snake $s _ i$ 放大：如果snake $s _ i$ 占用单元格 $[l, r]$，它扩大到一段 $[l, r + 1]$

-snake $s _ i$ 收缩：如果snake s _ i$ 占据了单元格 $[l, r]$ ，则它收缩为一个段 $[l + 1, r]$ 。每一秒钟，都有一个事件发生。

如果在任何时候，任何一条蛇遇到了障碍(另一条蛇或长带的末端)，你就输了。

否则，您的得分等于到目前为止任何蛇所占据的最大单元格。

你能达到的最低分数是多少？


**Input**

The first line contains two integers $n$ and $q$ ($1 \le n \le 20$; $1 \le q \le 2 \cdot 10^5$) — the number of snakes and the number of events. Next $q$ lines contain the description of events — one per line.

The $i$\-th line contains

-   either "$s_i$ +" ($1 \le s_i \le n$) meaning that the $s_i$\-th snake enlarges
-   or "$s_i$ \-" ($1 \le s_i \le n$) meaning that the $s_i$\-th snake shrinks.

Additional constraint on the input: the given sequence of events is valid, i. e. a snake of length $1$ never shrinks.



第一行包含两个整数 $n$ 和 $q$ ( $1 \le n \le 20$ $1 \le q \le 2 \cdot 10^5$ )—蛇的数量和事件的数量。

接下来的 $q$ 行包含事件的描述—每行一个。

第 $i$ 行包含

-“ $s _ i$ +”( $1 \le s _ i \le n$ ) 这意味着第 $s _i$ 条蛇变大了

-或“ $s _ i$ \-”( $1 \le s _ i \le n$ )表示第 $s _; i$ 条蛇缩小。

对输入的附加约束：给定的事件序列是有效的，即有长度的蛇永远不会收缩。



**Output**

Print one integer — the minimum possible score.

打印一个整数-可能的最小分数。


**Example**

Input

3 6
1 +
1 -
3 +
3 -
2 +
2 -


Output

4

Input

5 13
5 +
3 +
5 -
2 +
4 +
3 +
5 +
5 -
2 +
3 -
3 +
3 -
2 +



Output

11

**Note**

In the first test, the optimal strategy is to place the second snake at cell $1$, the third snake — at $2$, and the first one — at $3$. The maximum occupied cell is cell $4$, and it's the minimum possible score.

In the second test, one of the optimal strategies is to place:

-   snake $2$ at position $1$;
-   snake $3$ at position $4$;
-   snake $5$ at position $6$;
-   snake $1$ at position $9$;
-   snake $4$ at position $10$.


在第一次测试中，最佳策略是将第二条蛇放置在 $1$ 单元格，第三条蛇放置在 $2$ 单元格，第一条蛇放置在 $3$ 单元格。最大占用单元格是 4$ 单元格，这也是可能的最小得分。

在第二次测试中，最佳策略之一是放置：

- 蛇 $2$ 位于位置 $1$ ；
- 蛇 $3$ 位于位置 $4$ ；
- 蛇 $5$ 位于位置 $6$ ；
- 蛇$9$ 位于位置 $1$ ；
- 蛇 $10$ 位于位置 $4$ 。

### 题解
**本题的分数是从最左端的蛇左端点到到最右端的蛇的右端点的长度**

为了让分数尽可能低，我们应当让蛇之间的间距尽可能的小（即不让游戏输取得最小值）。

对于确定的排列，我们让每条蛇之间的距离都取最小值，可以得到答案为$1  + \sum dis + last$（$[1, 2], [3,4]$两条蛇的距离定义为$1$, $last$为最后一条蛇操作$+$的个数。）

首先考虑如何求$min_{i, j}$(将 $j$ 放在 $i$ 后面最小的距离)

- 对于确定的 $(i, j)$ ，初始距离为$1$，此时至少需要$1$的距离，遍历 $q$ 个操作：遇到 $i +$操作，将距离 $-1$，如果距离变为 $0$，则意味着此时至少需要的距离要 $+1$， 重新设置距离为 $1$ ；遇到 $j -$操作，将距离 $+1$。最后至少需要的距离则为$min_{i, j}$

接下来，状压$dp$ 求得最小值，有转移方程 $dp[s \cup k][k] = min(dp[s][j] + mindis[j][k])$($j$为$s$状态下未取过的点)。

最后的答案为$min(dp[(1<<n)-1][i] + last[i])$($0 \le i \le n-1$, $last[i]$为蛇$i$操作$+$的个数.) 

代码如下

```cpp
#include <bits/stdc++.h>
using namespace std;
      
typedef long long ll;
const ll inf =  0x3f3f3f3f;


inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
       
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
       
void print(ll x){pt(x), puts("");}


int main(){
    ll n = read(), q = read();
    vector<pair<ll, char>> ops(q);
    for(ll i=0;i<q;i++){
        ops[i].first = read() - 1;
        ops[i].second = getchar();
    }

    vector<vector<ll>> mindis(n, vector<ll>(n, 0));
    ll dis, need;
    for(ll i=0;i<n;i++){
        for(ll j=0;j<n;j++){
            if (i!= j){
                dis = 1;
                need = 1;
                for(auto op:ops){
                    if (op.first == i && op.second == '+'){
                        dis --;
                        if (dis == 0){
                            need ++;
                            dis ++;
                        }
                    }
                    else if(op.first == j && op.second == '-'){
                        dis ++;
                    }
                }
                mindis[i][j] = need;
            }
        }
    }
    
    vector<ll> last(n, 0);
    for(ll i=0;i<n;i++){
        for(auto op:ops){
            if (op.first == i && op.second == '+'){
                last[i] ++;
            }
        }
    }

    vector<vector<ll>> dp(1<<n, vector<ll>(n, inf));
    for(ll i=0;i<n;i++){
        dp[1<<i][i] = 1;
    }
    for(ll i=0;i<1<<n;i++){
        for(ll j=0;j<n;j++){
            if (i>>j&1){
                for(ll k=0;k<n;k++){
                    if (!(i>>k&1)){
                        ll news = i|1<<k;
                        dp[news][k] = min(dp[news][k], dp[i][j] + mindis[j][k]);
                    }
                }
            }
        }
    }

    ll ans = inf;
    for(ll i=0;i<n;i++){
        ans = min(ans, dp[(1<<n)-1][i] + last[i]);
    }
    print(ans);
}
```

终于把题补完了(2024/12/16 1:10)

![提交记录](https://i-blog.csdnimg.cn/direct/c76b4a00effd4f08bc714ca13bf2dca1.png)