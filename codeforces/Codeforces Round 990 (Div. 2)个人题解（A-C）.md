 **tip:所有翻译均为机翻（部分影响理解的翻译错误做了修改）** 

[Codeforces Round 990 (Div. 2)](https://codeforces.com/contest/2047)

 **暂时包含A-C**

# A. Alyona and a Square Jigsaw Puzzle

**time limit per test:1 second**

**memory limit per test:256 megabytes**

[2047A](https://codeforces.com/contest/2047/problem/A)



## 原题

Alyona assembles an unusual square Jigsaw Puzzle. She does so in N days in the following manner:

\-  On the first day, she starts by placing the central piece in the center of the table.
 \-  On each day after the first one, she places a certain number of pieces around the central piece in clockwise order, always finishing each square layer completely before starting a new one.

For example, she places the first 14 pieces in the following order:

![e42c169f5c8a4cf7aa791cffd97d09eb.png](https://i-blog.csdnimg.cn/direct/e42c169f5c8a4cf7aa791cffd97d09eb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑The colors denote the layers. The third layer is still unfinished.

Alyona is happy if at the end of the day the assembled part of the puzzle does not have any started but unfinished layers. Given the number of pieces she assembles on each day, find the number of days Alyona is happy on.



阿廖娜组装了一个不寻常的方形拼图。她以下列方式在 n 天内完成此项工作：

-在第一天，她首先把中间的那块放在桌子的中央。
 -在第一个之后的每一天，她将一定数量的碎片按顺时针顺序放置在中心碎片周围，总是在开始一个新的方块之前完成每个正方形图层。

例如，她将第一个 14块按以下顺序排列：

![e42c169f5c8a4cf7aa791cffd97d09eb.png](https://i-blog.csdnimg.cn/direct/e42c169f5c8a4cf7aa791cffd97d09eb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑颜色表示层。第三层还没有完成。

如果在一天结束时，谜题的组装部分没有任何开始但未完成的层，Alyona就会很高兴。给定她每天组装的零件的数量，找出Alyona快乐的天数。



**Input**

Each test contains multiple test cases. The first line contains the number of test cases t (![eq?%241%20%5Cle%20t%20%5Cle%20500%24](https://latex.csdn.net/eq?%241%20%5Cle%20t%20%5Cle%20500%24)). The description of the test cases follows.

The first line contains a single integer n (![eq?%241%20%5Cle%20n%20%5Cle%20100%24](https://latex.csdn.net/eq?%241%20%5Cle%20n%20%5Cle%20100%24)), the number of days.

The second line contains $n$ integers ![eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24](https://latex.csdn.net/eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24) (![eq?%241%20%5Cle%20a_i%20%5Cle%20100%24](https://latex.csdn.net/eq?%241%20%5Cle%20a_i%20%5Cle%20100%24), ![eq?%24a_1%20%3D%201%24](https://latex.csdn.net/eq?%24a_1%20%3D%201%24)), where ![eq?%24a_i%24](https://latex.csdn.net/eq?%24a_i%24) is the number of pieces Alyona assembles on the i-th day.



It is guaranteed in each test case that at the end of the $n$ days, there are no unfinished layers.



每个测试包含多个测试用例。第一行包含测试用例的数量 t (![eq?%241%20%5Cle%20t%20%5Cle%20500%24](https://latex.csdn.net/eq?%241%20%5Cle%20t%20%5Cle%20500%24))。下面是测试用例的描述。

第一行包含一个整数 n (![eq?%241%20%5Cle%20n%20%5Cle%20100%24](https://latex.csdn.net/eq?%241%20%5Cle%20n%20%5Cle%20100%24))，表示天数。

第二行包含 n 个整数 ![eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24](https://latex.csdn.net/eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24) (![eq?%241%20%5Cle%20a_i%20%5Cle%20100%24](https://latex.csdn.net/eq?%241%20%5Cle%20a_i%20%5Cle%20100%24), ![eq?%24a_1%20%3D%201%24](https://latex.csdn.net/eq?%24a_1%20%3D%201%24))，其中 ![eq?%24a_i%24](https://latex.csdn.net/eq?%24a_i%24) 是Alyona在第 i 天组装的碎片数。

在每个测试用例中，保证在 n 天结束时，没有未完成的层。



 **Output**

For each test case, print a single integer: the number of days when Alyona is happy.

对于每个测试用例，打印一个整数：Alyona快乐的天数。



**Example**

Input

5
 1
 1
 2
 1 8
 5
 1 3 2 1 2
 7
 1 2 1 10 2 7 2
 14
 1 10 10 100 1 1 10 1 10 2 10 2 10 1
 

Output

1
 2
 2
 2
 3
 

## 题解

当放置过的方块的数量等于![eq?%282n-1%29%5E2%2Cn%5Cin%20N%5E*](https://latex.csdn.net/eq?%282n-1%29%5E2%2Cn%5Cin%20N%5E*)时， 第n层刚好被填满， 快乐的天数加一。

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
    ll n = read();
    vector<ll> a(n, 0);
    for(ll i=0;i<n;i++){
        a[i] = read();
    }
    ll ans = 0;
    ll cnt = 0;
    ll need = (2*cnt+1)*(2*cnt+1);
    ll did = 0;
    for(ll i=0;i<n;i++){
        did += a[i];
        while (did>=need){
            if (did == need){
                ans ++;
            }
            cnt += 1;
            need = (2*cnt+1)*(2*cnt+1);
        }
    }
    print(ans);
}


int main(){
    ll t= read();
    while (t--){
        solve();
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)





# B. Replace Character

**time limit per test:1 second**

**memory limit per test:256 megabytes**

[2047B](https://codeforces.com/contest/2047/problem/B#)



## **原题**

You're given a string s of length n, consisting of only lowercase English letters.

You must do the following operation exactly once:

\-  Choose any two indices i and j (![eq?%241%20%5Cle%20i%2C%20j%20%5Cle%20n%24](https://latex.csdn.net/eq?%241%20%5Cle%20i%2C%20j%20%5Cle%20n%24)). You can choose ![eq?%24i%20%3D%20j%24](https://latex.csdn.net/eq?%24i%20%3D%20j%24).
 \-  Set ![eq?%24s_i%20%3A%3D%20s_j%24](https://latex.csdn.net/eq?%24s_i%20%3A%3D%20s_j%24).

You need to minimize the number of distinct permutations![eq?%24%5E%5Cdagger%24](https://latex.csdn.net/eq?%24%5E%5Cdagger%24) of s. Output any string with the smallest number of distinct permutations after performing **exactly one** operation.

![eq?%24%5E%5Cdagger%24](https://latex.csdn.net/eq?%24%5E%5Cdagger%24) A permutation of the string is an arrangement of its characters into any order. For example, "bac" is a permutation of "abc" but "bcc" is not.



给您一个长度为 n 的字符串 s ，仅由小写英文字母组成。

以下操作必须精确执行一次：

—选择任意两个索引 i 和 j (![eq?%241%20%5Cle%20i%2C%20j%20%5Cle%20n%24](https://latex.csdn.net/eq?%241%20%5Cle%20i%2C%20j%20%5Cle%20n%24))。您可以选择 ![eq?%24i%20%3D%20j%24](https://latex.csdn.net/eq?%24i%20%3D%20j%24) 。  ![eq?%24s_i%20%3A%3D%20s_j%24](https://latex.csdn.net/eq?%24s_i%20%3A%3D%20s_j%24)（将![eq?s_i](https://latex.csdn.net/eq?s_i)更改为![eq?s_j](https://latex.csdn.net/eq?s_j)）。

您需要最小化 s 的不同排列 † 的数量。在执行**一次**操作后，输出具有最少不同排列数的任何字符串。 

† 字符串的排列是将字符串中的字符按任意顺序排列。例如，“bac”是“abc”的排列，但“bcc”不是。 



**Input**



Each test contains multiple test cases. The first line contains the number of test cases t (![eq?%241%20%5Cle%20t%20%5Cle%20500%24](https://latex.csdn.net/eq?%241%20%5Cle%20t%20%5Cle%20500%24)). The description of the test cases follows.

The first line of each test case contains n (![eq?%241%20%5Cle%20n%20%5Cle%2010%24](https://latex.csdn.net/eq?%241%20%5Cle%20n%20%5Cle%2010%24)) — the length of string s.

The second line of each test case contains s of length n. The string contains only lowercase English letters.



每个测试包含多个测试用例。第一行包含测试用例的数量t (![eq?%241%20%5Cle%20t%20%5Cle%20500%24](https://latex.csdn.net/eq?%241%20%5Cle%20t%20%5Cle%20500%24))。下面是测试用例的描述。

每个测试用例的第一行包含字符串 s 的长度 n (![eq?%241%20%5Cle%20n%20%5Cle%2010%24](https://latex.csdn.net/eq?%241%20%5Cle%20n%20%5Cle%2010%24)) 。

每个测试用例的第二行包含长度为 n 的 s$ 。字符串中只包含小写英文字母。



**Output**

For each test case, output the required s after applying exactly one operation. If there are multiple solutions, print any of them.



对于每个测试用例，在应用一个操作后输出所需的 s 。如果有多个解决方案，打印其中任何一个。



**Example**

Input

6
 3
 abc
 4
 xyyx
 8
 alphabet
 1
 k
 10
 aabbccddee
 6
 ttbddq
 

Output

cbc
 yyyx
 alphaaet
 k
 eabbccddee
 tttddq

##   题解

字符串的排列数量不收其字符顺序的影响。

设某个字符串（长度为n）中有 ![eq?a_1](https://latex.csdn.net/eq?a_1)个![eq?x_1](https://latex.csdn.net/eq?x_1)字符....![eq?a_m](https://latex.csdn.net/eq?a_m)个![eq?x_m](https://latex.csdn.net/eq?x_m)字符

则排列的数量为 ![eq?%5Cfrac%7BA_%7Bn%7D%5E%7Bn%7D%7D%7B%5Cprod_%7Bj%3D1%7D%5E%7Bm%7D%20A_%7Ba_j%7D%5E%7Ba_j%7D%7D](https://latex.csdn.net/eq?%5Cfrac%7BA_%7Bn%7D%5E%7Bn%7D%7D%7B%5Cprod_%7Bj%3D1%7D%5E%7Bm%7D%20A_%7Ba_j%7D%5E%7Ba_j%7D%7D)

不妨考虑字符串![eq?aaaabbbccd](https://latex.csdn.net/eq?aaaabbbccd)，初始排列数量为 ![eq?%5Cfrac%7BA_%7B10%7D%5E%7B10%7D%7D%7BA_%7B4%7D%5E%7B4%7D%20%5Ctimes%20A_%7B3%7D%5E%7B3%7D%20%5Ctimes%20A_%7B2%7D%5E%7B2%7D%20%5Ctimes%20A_%7B1%7D%5E%7B1%7D%7D%20%3D%2012600](https://latex.csdn.net/eq?%5Cfrac%7BA_%7B10%7D%5E%7B10%7D%7D%7BA_%7B4%7D%5E%7B4%7D%20%5Ctimes%20A_%7B3%7D%5E%7B3%7D%20%5Ctimes%20A_%7B2%7D%5E%7B2%7D%20%5Ctimes%20A_%7B1%7D%5E%7B1%7D%7D%20%3D%2012600)，在更改的过程中分子不会变化，因此我们需要让分母尽可能大。

不难发现， 将出现次数最少的d换为出现次数最多的a，排列数量为 ![eq?%5Cfrac%7BA_%7B10%7D%5E%7B10%7D%7D%7BA_%7B5%7D%5E%7B5%7D%20%5Ctimes%20A_%7B3%7D%5E%7B3%7D%20%5Ctimes%20A_%7B2%7D%5E%7B2%7D%20%7D%3D%202520](https://latex.csdn.net/eq?%5Cfrac%7BA_%7B10%7D%5E%7B10%7D%7D%7BA_%7B5%7D%5E%7B5%7D%20%5Ctimes%20A_%7B3%7D%5E%7B3%7D%20%5Ctimes%20A_%7B2%7D%5E%7B2%7D%20%7D%3D%202520)。

我们只需找到出现次数最多的字符，用它去替换一个出现次数最少的字符。

代码如下

python

```python
t = int(input())
for _ in range(t):
    n = int(input())
    s = input()
    m = {}
    for i in s:
         m[i] = m.get(i, 0) + 1
    values = sorted([(i, m[i]) for i in m],key=lambda x:x[1], reverse=True)
    print(s.replace(values[-1][0], values[0][0], 1))
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

c++ 

```cpp
#include <bits/stdc++.h>
using namespace std;
  
typedef long long ll;
typedef pair<long long,long long> PLL;
  
inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
   
bool cmp(PLL x, PLL y){
    return x.second > y.second;
}
void solve(){
    ll n = read();
    char s[20];
    map<ll, ll> m;
    for(ll i=0;i<n;i++){
        s[i] = getchar();
        m[s[i]] ++ ;
    }
    vector<PLL> values;
    for(auto pair:m){
        values.push_back(pair);
    }
    ll len = values.size();
    sort(values.begin(), values.end(), cmp);
    for(ll i=0;i<n;i++){
        if (s[i] == values[len-1].first){
            s[i] = values[0].first;
            break;
        }
    }
    for(ll i=0;i<n;i++){
        putchar(s[i]);
    }
    putchar('\n');

}

int main(){
    ll t = read();
    while(t--){
        solve();
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# C. Swap Columns and Find a Path

**time limit per test:2 second**

**memory limit per test:512 megabytes**

[2047C](https://codeforces.com/contest/2047/problem/C)

## 

## 原题

There is a matrix consisting of 2 rows and n columns. The rows are numbered from 1 to 2 from top to bottom; the columns are numbered from 1 to n from left to right. Let's denote the cell on the intersection of the i-th row and the j-th column as ![eq?%24%28i%2Cj%29%24](https://latex.csdn.net/eq?%24%28i%2Cj%29%24). Each cell contains an integer; initially, the integer in the cell ![eq?%24%28i%2Cj%29%24](https://latex.csdn.net/eq?%24%28i%2Cj%29%24) is ![eq?%24a_%7Bi%2Cj%7D%24](https://latex.csdn.net/eq?%24a_%7Bi%2Cj%7D%24).

You can perform the following operation any number of times (possibly zero):

\-  choose two columns and swap them (i. e. choose two integrs x and y such that![eq?%241%20%5Cle%20x%20%3C%20y%20%5Cle%20n%24](https://latex.csdn.net/eq?%241%20%5Cle%20x%20%3C%20y%20%5Cle%20n%24), then swap ![eq?%24a_%7B1%2Cx%7D%24](https://latex.csdn.net/eq?%24a_%7B1%2Cx%7D%24) with , and then swap ![eq?%24a_%7B2%2Cx%7D%24](https://latex.csdn.net/eq?%24a_%7B2%2Cx%7D%24) with ![eq?%24a_%7B2%2Cy%7D%24](https://latex.csdn.net/eq?%24a_%7B2%2Cy%7D%24)).

After performing the operations, you have to choose a path from the cell ![eq?%24%281%2C1%29%24](https://latex.csdn.net/eq?%24%281%2C1%29%24) to the cell ![eq?%24%282%2Cn%29%24](https://latex.csdn.net/eq?%24%282%2Cn%29%24). For every cell ![eq?%24%28i%2Cj%29%24](https://latex.csdn.net/eq?%24%28i%2Cj%29%24) in the path except for the last, the next cell should be either ![eq?%24%28i&plus;1%2Cj%29%24](https://latex.csdn.net/eq?%24%28i&plus;1%2Cj%29%24) or ![eq?%24%28i%2Cj&plus;1%29%24](https://latex.csdn.net/eq?%24%28i%2Cj&plus;1%29%24). Obviously, the path cannot go outside the matrix.

The cost of the path is the sum of all integers in all ![eq?%24%28n&plus;1%29%24](https://latex.csdn.net/eq?%24%28n&plus;1%29%24) cells belonging to the path. You have to perform the operations and choose a path so that its cost is **maximum** possible.



有一个由 2 行和 n 列组成的矩阵。行从上到下编号为 1 到 2 ；列从左到右编号为 1 到 n 。我们将位于 第i 行和 第j 列交点上的单元格表示为 ![eq?%24%28i%2Cj%29%24](https://latex.csdn.net/eq?%24%28i%2Cj%29%24) 。每个单元格包含一个整数；最初，单元格 ![eq?%24%28i%2Cj%29%24](https://latex.csdn.net/eq?%24%28i%2Cj%29%24) 中的整数是 ![eq?%24a_%7Bi%2Cj%7D%24](https://latex.csdn.net/eq?%24a_%7Bi%2Cj%7D%24) 。

您可以执行以下操作任意次数(可能为零)：

-选择两列并交换它们(即：选择两个整数 x 和 y 使得 ![eq?1%20%5Cle%20x%20%3C%20y%20%5Cle%20n](https://latex.csdn.net/eq?1%20%5Cle%20x%20%3C%20y%20%5Cle%20n) ，然后将 ![eq?%24a_%7B1%2Cx%7D%24](https://latex.csdn.net/eq?%24a_%7B1%2Cx%7D%24) 与 ![eq?%24a_%7B1%2Cy%7D%24](https://latex.csdn.net/eq?%24a_%7B1%2Cy%7D%24)交换，然后将 ![eq?%24a_%7B2%2Cx%7D%24](https://latex.csdn.net/eq?%24a_%7B2%2Cx%7D%24) 与 ![eq?%24a_%7B2%2Cy%7D%24](https://latex.csdn.net/eq?%24a_%7B2%2Cy%7D%24) 交换)。

操作完成后，需要选择从单元格 ![eq?%24%281%2C1%29%24](https://latex.csdn.net/eq?%24%281%2C1%29%24) 到单元格 ![eq?%24%282%2Cn%29%24](https://latex.csdn.net/eq?%24%282%2Cn%29%24) 的路径。对于路径中除最后一个单元格之外的每个单元格 ![eq?%24%28i%2Cj%29%24](https://latex.csdn.net/eq?%24%28i%2Cj%29%24) ，下一个单元格应该是 ![eq?%24%28i&plus;1%2Cj%29%24](https://latex.csdn.net/eq?%24%28i&plus;1%2Cj%29%24) 或 ![eq?%24%28i%2Cj&plus;1%29%24](https://latex.csdn.net/eq?%24%28i%2Cj&plus;1%29%24) 。很明显，路径不能走出矩阵。

路径的代价是属于该路径的所有 ![eq?%24%28n&plus;1%29%24](https://latex.csdn.net/eq?%24%28n&plus;1%29%24) 单元格中所有整数的和。你必须执行操作并选择一条路径，使它的代价是**最大**的。



**Input**

Each test contains multiple test cases. The first line contains the number of test cases t (![eq?%241%20%5Cle%20t%20%5Cle%205000%24](https://latex.csdn.net/eq?%241%20%5Cle%20t%20%5Cle%205000%24)). The description of the test cases follows.



Each test case consists of three lines:

\- the first line contains one integer n (![eq?%241%20%5Cle%20n%20%5Cle%205000%24](https://latex.csdn.net/eq?%241%20%5Cle%20n%20%5Cle%205000%24))— the number of columns in the matrix;

\- the second line contains n integers ![eq?%24a_%7B1%2C1%7D%2C%20a_%7B1%2C2%7D%2C%20%5Cldots%2C%20a_%7B1%2Cn%7D%24](https://latex.csdn.net/eq?%24a_%7B1%2C1%7D%2C%20a_%7B1%2C2%7D%2C%20%5Cldots%2C%20a_%7B1%2Cn%7D%24) (![eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24](https://latex.csdn.net/eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24)) — the first row of the matrix;

\- the third line contains n integers ![eq?%24a_%7B2%2C1%7D%2C%20a_%7B2%2C2%7D%2C%20%5Cldots%2C%20a_%7B2%2Cn%7D%24](https://latex.csdn.net/eq?%24a_%7B2%2C1%7D%2C%20a_%7B2%2C2%7D%2C%20%5Cldots%2C%20a_%7B2%2Cn%7D%24) (![eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24](https://latex.csdn.net/eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24)) — the second row of the matrix.

It is guaranteed that the sum of n over all test cases does not exceed 5000.



每个测试包含多个测试用例。第一行包含测试用例的数量 t (![eq?%241%20%5Cle%20t%20%5Cle%205000%24](https://latex.csdn.net/eq?%241%20%5Cle%20t%20%5Cle%205000%24))。下面是测试用例的描述。

每个测试用例由三行组成：

-第一行包含一个整数 n (![eq?%241%20%5Cle%20n%20%5Cle%205000%24](https://latex.csdn.net/eq?%241%20%5Cle%20n%20%5Cle%205000%24))-矩阵中的列数；
 -第二行包含 n 个整数![eq?%24a_%7B1%2C1%7D%2C%20a_%7B1%2C2%7D%2C%20%5Cldots%2C%20a_%7B1%2Cn%7D%24](https://latex.csdn.net/eq?%24a_%7B1%2C1%7D%2C%20a_%7B1%2C2%7D%2C%20%5Cldots%2C%20a_%7B1%2Cn%7D%24) (![eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24](https://latex.csdn.net/eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24))-矩阵的第一行；
 -第三行包含 n个整数 ![eq?%24a_%7B2%2C1%7D%2C%20a_%7B2%2C2%7D%2C%20%5Cldots%2C%20a_%7B2%2Cn%7D%24](https://latex.csdn.net/eq?%24a_%7B2%2C1%7D%2C%20a_%7B2%2C2%7D%2C%20%5Cldots%2C%20a_%7B2%2Cn%7D%24) (![eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24](https://latex.csdn.net/eq?%24-10%5E5%20%5Cle%20a_%7Bi%2Cj%7D%20%5Cle%2010%5E5%24)) -矩阵的第二行。

保证所有测试用例 n 的和不超过 5000 。



**Output**

For each test case, print one integer — the maximum cost of a path you can obtain.



对于每个测试用例，打印一个整数—您可以获得的路径的最大代价。



**Example**

Input

3
 1
 -10
 5
 3
 1 2 3
 10 -5 -3
 4
 2 8 5 3
 1 10 3 4

Output

-5
 16
 29

**Note**

Here are the explanations of the first three test cases of the example. The left matrix is the matrix given in the input, the right one is the state of the matrix after several column swaps (possibly zero). The optimal path is highlighted in green.



下面是对该示例的前三个测试用例的解释。左边的矩阵是输入中给出的矩阵，右边的矩阵是经过几列交换(可能为零)后的矩阵状态。最优路径用绿色突出显示。

![880f077d53a54630bf5f2149567c13fc.png](https://i-blog.csdnimg.cn/direct/880f077d53a54630bf5f2149567c13fc.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑



## **题解**

考虑到只能向下和向右走，可将整个路径分为 ![eq?a_%7B1%2C%201%7D%20%5Crightarrow%20a_%7B1%2C%20m%7D%2C%20a_%7B1%2C%20m%7D%20%5Crightarrow%20a_%7B2%2C%20m%7D%2C%20a_%7B2%2C%20m%7D%20%5Crightarrow%20a_%7B2%2C%20n%7D](https://latex.csdn.net/eq?a_%7B1%2C%201%7D%20%5Crightarrow%20a_%7B1%2C%20m%7D%2C%20a_%7B1%2C%20m%7D%20%5Crightarrow%20a_%7B2%2C%20m%7D%2C%20a_%7B2%2C%20m%7D%20%5Crightarrow%20a_%7B2%2C%20n%7D)三部分

因为可以无限次交换，我们一定可以将![eq?a_%7B1%2C%20j%7D%20%3E%20a_%7B2%2C%20j%7D](https://latex.csdn.net/eq?a_%7B1%2C%20j%7D%20%3E%20a_%7B2%2C%20j%7D)的列放到左边， ![eq?a_%7B1%2C%20j%7D%20%5Cleqslant%20a_%7B2%2C%20j%7D](https://latex.csdn.net/eq?a_%7B1%2C%20j%7D%20%5Cleqslant%20a_%7B2%2C%20j%7D) 的列放到右边

即我们一定可以构造出一种情况，使得路径能够取到每一列中的最大值。

考虑从第一行到第二行的过程：我们可以选择一列中较小数最大的那一列，将它放在中间。

这样构造出来的即为所求路径。

（答案实际上为![eq?%5Csum%20_%7Bt%3D1%7D%5E%7Bn%7D%20max%28a_%7B1%2C%20t%7D%2C%20a_%7B2%2C%20t%7D%29%20&plus;%20max%28%5C%7Bmin%28a_%7B1%2C%20t%7D%2C%20a_%7B2%2C%20t%7D%20%29%2C%20t%20%5Cin%20%5B1%2C%20n%5D%20%5C%7D%29](https://latex.csdn.net/eq?%5Csum%20_%7Bt%3D1%7D%5E%7Bn%7D%20max%28a_%7B1%2C%20t%7D%2C%20a_%7B2%2C%20t%7D%29%20&plus;%20max%28%5C%7Bmin%28a_%7B1%2C%20t%7D%2C%20a_%7B2%2C%20t%7D%20%29%2C%20t%20%5Cin%20%5B1%2C%20n%5D%20%5C%7D%29)）

代码如下

```cpp
#include <bits/stdc++.h>
using namespace std;
  
typedef long long ll;
const ll INF = INT_MAX;

  
inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
   
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
   
void print(ll x){pt(x), puts("");}


void solve(){
    ll n = read();
    ll a[3][5009];
    for(ll x=0;x<=1;x++){
        for(ll y=0;y<n;y++){
            a[x][y] = read();
        }
    }
    ll total =0;
    ll m = -INF;
    for(ll i=0;i<n;i++){
        total += max(a[0][i], a[1][i]);
        m = max(m, min(a[0][i], a[1][i]));
    }
    print(total + m);
}



int main(){
    ll t = read();
    while(t--){
        solve();
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)