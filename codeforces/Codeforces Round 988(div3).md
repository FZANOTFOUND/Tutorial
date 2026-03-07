 tip:所有翻译均为机翻（部分影响理解的翻译错误做了修改）

目前包括A~E(2024/11/21)

![d0b65880c55143deb18515d773e73deb.png](https://i-blog.csdnimg.cn/direct/d0b65880c55143deb18515d773e73deb.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

目前包含A~E 和 G(2024/11/23)（两个小时终于把G题搞定了）

![7c1f4384d2714efbac0c72df63cba89a.png](https://i-blog.csdnimg.cn/direct/7c1f4384d2714efbac0c72df63cba89a.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

包含A~G（2024/11/26）

题目里的图片是私货（文章末尾会附上链接

![d71a39ae74fa462f8b4d44940700bb59.png](https://i-blog.csdnimg.cn/direct/d71a39ae74fa462f8b4d44940700bb59.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

# A. Twice

**dificulty:800**

**time limit per test:1 second**

**memory limit per test:256 megabytes**

![img](https://i-blog.csdnimg.cn/direct/d7d30c59ca7d44bf94c6626a3b5fcaec.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

[Problem - A - Codeforces](https://codeforces.com/contest/2037/problem/A)

## 原题

Kinich wakes up to the start of a new day. He turns on his phone, checks his mailbox, and finds a mysterious present. He decides to unbox the present.

Kinich unboxes an array a with n integers. Initially, Kinich's score is 0. He will perform the following operation any number of times:

​    **·**Select two indices i and j (![eq?1%5Cleq%20i%20%5Cleq%20j%20%5Cleq%20n](https://latex.csdn.net/eq?1%5Cleq%20i%20%5Cleq%20j%20%5Cleq%20n))such that neither i nor j has been chosen in any previous operation and ![eq?a_i%20%3D%20a_j](https://latex.csdn.net/eq?a_i%20%3D%20a_j). Then, add 1 to his score.

Output the maximum score Kinich can achieve after performing the aforementioned operation any number of times.



基尼奇醒来迎接新的一天的开始。他打开手机，查看邮箱，发现了一份神秘的礼物。他决定打开礼物的盒子。

基尼奇打开了一个有n个元素的数组 a 。最初，基尼奇的分数是 0 。他将执行任意次数的以下操作：

—选择两个索引 i 和 j (![eq?1%5Cleq%20i%20%5Cleq%20j%20%5Cleq%20n](https://latex.csdn.net/eq?1%5Cleq%20i%20%5Cleq%20j%20%5Cleq%20n))，确保在之前的操作中既没有选择 i 也没有选择 j 和 ![eq?a_i%20%3D%20a_j](https://latex.csdn.net/eq?a_i%20%3D%20a_j) 。然后，在他的分数上加上 1 。

输出Kinich在执行上述操作任意次数后可以获得的最大分数。



**Input**

The first line contains an integer t (![eq?1%5Cleq%20t%5Cleq%20500](https://latex.csdn.net/eq?1%5Cleq%20t%5Cleq%20500)) — the number of test cases.

The first line of each test case contains an integer n (![eq?1%5Cleq%20n%5Cleq%2020](https://latex.csdn.net/eq?1%5Cleq%20n%5Cleq%2020)) — the length of a.

The following line of each test case contains n space-separated integers![eq?a_1%2Ca_2%2C......%2Ca_n%281%5Cleq%20a_i%5Cleq%20n%29](https://latex.csdn.net/eq?a_1%2Ca_2%2C......%2Ca_n%281%5Cleq%20a_i%5Cleq%20n%29).



第一行包含一个整数 t (![eq?1%5Cleq%20t%5Cleq%20500](https://latex.csdn.net/eq?1%5Cleq%20t%5Cleq%20500)) —测试用例的数量。

每个测试用例的第一行包含一个整数 n (![eq?1%5Cleq%20n%5Cleq%2020](https://latex.csdn.net/eq?1%5Cleq%20n%5Cleq%2020)) ——a的长度。

每个测试用例的下一行包含 n 个空格分隔的整数![eq?a_1%2Ca_2%2C......%2Ca_n%281%5Cleq%20a_i%5Cleq%20n%29](https://latex.csdn.net/eq?a_1%2Ca_2%2C......%2Ca_n%281%5Cleq%20a_i%5Cleq%20n%29)。



**Output**

For each test case, output the maximum score achievable on a new line.



对于每个测试用例，在新的一行上输出可实现的最大分数。



**Example**

Input

5
 1
 1
 2
 2 2
 2
 1 2
 4
 1 2 3 1
 6
 1 2 3 1 2 3

OutPut
 0
 1
 0
 1
 3

## 题解

对于某个数t，若其在a中出现的次数为n，不难想到其最大可构造的匹配数量为![eq?%5Cleft%20%5Clfloor%20%5Cfrac%7Bn%7D%7B2%7D%20%5Cright%20%5Crfloor](https://latex.csdn.net/eq?%5Cleft%20%5Clfloor%20%5Cfrac%7Bn%7D%7B2%7D%20%5Cright%20%5Crfloor)。

遍历a，将数据出现次数用哈希表统计，再求![eq?%5Csum_%7Bi%5Cin%20hashmap.keys%7D%5E%7B%7D%20%5Cleft%20%5Clfloor%20%5Cfrac%7Bhashmap%5Bi%5D%7D%7B2%7D%20%5Cright%20%5Crfloor](https://latex.csdn.net/eq?%5Csum_%7Bi%5Cin%20hashmap.keys%7D%5E%7B%7D%20%5Cleft%20%5Clfloor%20%5Cfrac%7Bhashmap%5Bi%5D%7D%7B2%7D%20%5Cright%20%5Crfloor)

代码如下

```python
t = int(input())
for _ in range(t):
    Map = {}
    n = int(input())
    a = list(map(int, input().split()))
    for i in a:
        Map[i] = Map.get(i, 0) + 1
    count = 0
    for key in Map:
        count += Map[key]//2
    print(count)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# B. Intercepted Inputs

**dificulty:800**

**time limit per test:2 seconds**

**memory limit per test:256 megabytes**

![img](https://i-blog.csdnimg.cn/direct/fbc1a251b0824a518f89739e174e5a78.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

[Problem - b - Codeforces](https://codeforces.com/contest/2037/problem/b)

## 原题

To help you prepare for your upcoming Codeforces contest, Citlali set a grid problem and is trying to give you a n by m grid through your input stream. Specifically, your input stream should contain the following:

   **·**The first line contains two integers n and m — the dimensions of the grid.

   **·**The following n lines contain m integers each — the values of the grid.

However, someone has intercepted your input stream, shuffled all given integers, and put them all on one line! Now, there are k integers all on one line, and you don't know where each integer originally belongs. Instead of asking Citlali to resend the input, you decide to determine the values of n and m yourself.

Output any possible value of n and m that Citlali could have provided.



为了帮助您为即将到来的Codeforces竞赛做准备，茜特菈莉设置了一个网格问题，并试图通过你的输入流为你提供一个 n × m 网格。具体来说，你的输入流应该包含以下内容：

​      **·**第一行包含两个整数 n 和 m -网格的尺寸。

​      **·**下面的 n 行每行包含 m 个整数—网格的值。

然而，有人截获了你的输入流，打乱了所有给定的整数，并把它们都放在一行上！现在，在一行中有 k 个整数，您不知道每个整数最初属于哪里。您决定自己确定 n 和 m 的值，而不是要求茜特菈莉重新发送输入。

输出茜特菈莉可能提供的 n 和 m 的任何可能值。



**Input**

The first line contains an integer t (![eq?1%5Cleq%20t%5Cleq%2010%5E4](https://latex.csdn.net/eq?1%5Cleq%20t%5Cleq%2010%5E4)) — the number of test cases.

The first line of each test case contains an integer k (![eq?3%5Cleq%20k%5Cleq%202%5Ctimes%2010%5E5](https://latex.csdn.net/eq?3%5Cleq%20k%5Cleq%202%5Ctimes%2010%5E5)) — the total number of inputs in your input stream.

The following line of each test case contains k integers ![eq?a_1%2Ca_2%2C......%2Ca_k](https://latex.csdn.net/eq?a_1%2Ca_2%2C......%2Ca_k) (![eq?1%20%5Cleq%20a_i%20%5Cleq%20k](https://latex.csdn.net/eq?1%20%5Cleq%20a_i%20%5Cleq%20k)) — the shuffled inputs of your input stream. It is guaranteed that n and m are contained within the k integers.

It is guaranteed that the sum of kk over all test cases does not exceed ![eq?2%20%5Ctimes%2010%5E5](https://latex.csdn.net/eq?2%20%5Ctimes%2010%5E5).



第一行包含一个整数 t (![eq?1%5Cleq%20t%5Cleq%2010%5E4](https://latex.csdn.net/eq?1%5Cleq%20t%5Cleq%2010%5E4))—测试用例的数量。

每个测试用例的第一行包含一个整数 k (![eq?3%5Cleq%20k%5Cleq%202%5Ctimes%2010%5E5](https://latex.csdn.net/eq?3%5Cleq%20k%5Cleq%202%5Ctimes%2010%5E5)) ——输入流中输入的总数。

每个测试用例的下面一行包含 k 个整数 ![eq?a_1%2Ca_2%2C......%2Ca_k](https://latex.csdn.net/eq?a_1%2Ca_2%2C......%2Ca_k) (![eq?1%20%5Cleq%20a_i%20%5Cleq%20k](https://latex.csdn.net/eq?1%20%5Cleq%20a_i%20%5Cleq%20k)) ——随机打乱的输入流。可以保证 n 和 m 包含在 k 整数中。

保证所有测试用例的 k 之和不超过 ![eq?2%20%5Ctimes%2010%5E5](https://latex.csdn.net/eq?2%20%5Ctimes%2010%5E5) 。



**Output**

For each test case, output two integers, one possible value of n and m. If multiple possible answers exist, output any.



对于每个测试用例，输出两个整数，其中一个可能值为 n 和 m 。如果存在多个可能的答案，则输出任意一个。



**Example**

Input

5
 3
 1 1 2
 11
 3 3 4 5 6 7 8 9 9 10 11
 8
 8 4 8 3 8 2 8 1
 6
 2 1 4 5 3 3
 8
 1 2 6 3 8 5 5 3
 

Output

1 1
 3 3
 2 3
 4 1
 1 6

## 题解

根据题意，我们需要再n个整数中找到两个整数 i, j 使得 ![eq?i%20%5Ctimes%20j%20%3D%20n-2](https://latex.csdn.net/eq?i%20%5Ctimes%20j%20%3D%20n-2)

遍历n-2的所有因子对，检查两个因子是否都在k个整数中。

要注意t最大为![eq?10%5E4](https://latex.csdn.net/eq?10%5E4),不能暴力遍历k个整数寻找i,j

（本场比赛绝大部分hack都是对B题的，基本都是tle）

python 代码（python的 a in list其实算的很快，用python没必要用其他的方法判断）

```python
t = int(input())
for _ in range(t):
    n = int(input())
    a = list(map(int, input().split()))
    for i in range(1,(n-2)//2+2):
        if (n-2)%i ==0:
            if i in a and (n-2)//i in a:
                print(i, (n-2)//i)
                break
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

c++代码（采用set来优化搜索）

```cpp
#include <iostream>
#include <set>
using namespace std;

int main()
{
    int t;
    cin>>t;
    while(t--)
    {   
        int n,t;
        cin>>n;
        set<int> appear;
        for(int i=0;i<n;i++)
        {
            cin>>t;
            appear.insert(t);
        }
        for(int i=1;i<=(n-2)/2+2;i++)
        {
            if ((n-2) % i == 0)
            {
                if (appear.find(i)!=appear.end()&&appear.find((n-2)/i)!=appear.end())
                {
                    cout<<i<<' '<<(n-2)/i<<endl;
                    break;
                }
            }
        }
    }
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# C.Superultra's Favorite Permutation

**dificulty:1000**

**time limit per test:2 seconds**

**memory limit per test:256 megabytes**



[Problem - C - Codeforces](https://codeforces.com/contest/2037/problem/C)

## **原题**

Superultra, a little red panda, desperately wants primogems. In his dreams, a voice tells him that he must solve the following task to obtain a lifetime supply of primogems. Help Superultra!

Construct a permutation∗ p of length （n such that ![eq?p_i%20&plus;%20p_%7Bi&plus;1%7D](https://latex.csdn.net/eq?p_i%20&plus;%20p_%7Bi&plus;1%7D) is composite† over all ![eq?1%5Cleq%20i%5Cleq%20n-1](https://latex.csdn.net/eq?1%5Cleq%20i%5Cleq%20n-1). If it's not possible, output −1.

∗A permutation of length n is an array consisting of n distinct integers from 1 to n in arbitrary order. For example, [2,3,1,5,4] is a permutation, but [1,2,2] is not a permutation (2 appears twice in the array), and [1,3,4]is also not a permutation (n=3 but there is 4 in the array).

†An integer x is composite if it has at least one other divisor besides 1 and x. For example, 4 is composite because 2 is a divisor.



Superultra，一只小熊猫，拼命想要原始宝石。在他的梦中，一个声音告诉他，他必须解决以下任务，以获得一生的原始宝石供应。帮助Superultra !

构造一个长度为 n 的排列∗ p ，使 所有![eq?p_i%20&plus;%20p_%7Bi&plus;1%7D](https://latex.csdn.net/eq?p_i%20&plus;%20p_%7Bi&plus;1%7D) ![eq?%281%5Cleq%20i%5Cleq%20n-1%29](https://latex.csdn.net/eq?%281%5Cleq%20i%5Cleq%20n-1%29) 都是合数 † 。如果不可能，输出 −1 。

*长度为 n 的排列是由 1 到 n 之间的任意顺序的不同整数 n 组成的数组。例如， [2,3,1,5,4]是一个排列，但 [1,2,2] 不是一个排列( 2 在数组中出现了两次)， [1,3,4] 也不是一个排列( n=3 但在数组中有 4 )。

† 如果一个整数 x 除了 1 和 x 之外至少有一个除数，那么它就是合数。例如， 4 是合数，因为 2 是一个除数。



**Input**

The first line contains![eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29](https://latex.csdn.net/eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29)— the number of test cases.

Each test case contains an integer ![eq?n%20%282%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%29](https://latex.csdn.net/eq?n%20%282%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%29)— the length of the permutation.

It is guaranteed that the sum of n over all test cases does not exceed ![eq?%242%20%5Ccdot%2010%5E5%24](https://latex.csdn.net/eq?%242%20%5Ccdot%2010%5E5%24).



第一行包含 ![eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29](https://latex.csdn.net/eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29)—测试用例的数量。

每个测试用例包含一个整数 ![eq?n%20%282%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%29](https://latex.csdn.net/eq?n%20%282%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%29)-排列的长度。

保证所有测试用例 n 的和不超过 $![eq?%242%20%5Ccdot%2010%5E5%24](https://latex.csdn.net/eq?%242%20%5Ccdot%2010%5E5%24) 。



**Output**

For each test case, if it's not possible to construct p, output -1 on a new line. Otherwise, output n integers![eq?%24p_1%2C%20p_2%2C%20%5Cldots%2C%20p_n%24](https://latex.csdn.net/eq?%24p_1%2C%20p_2%2C%20%5Cldots%2C%20p_n%24) on a new line.



对于每个测试用例，如果不可能构造 p ，则在另一行输出 −1 。否则，在另一行输出 n 个整数 ![eq?%24p_1%2C%20p_2%2C%20%5Cldots%2C%20p_n%24](https://latex.csdn.net/eq?%24p_1%2C%20p_2%2C%20%5Cldots%2C%20p_n%24) 。



**Example**

Input

2
 3
 8
 

Output

-1
 1 8 7 3 6 2 4 5



## **题解**

我们知道除了2以外的偶数都是合数，而奇数+奇数=偶数，偶数+偶数=偶数。因此我们可以把所有的奇数放在一起，所有的偶数放在一起。

接下来考虑奇数和偶数相接的地方如何为合数。

不难发现，最小的满足加起来是合数的奇偶数对是（4,5）。

因此将4,5放在中间，左边放偶数，右边放奇数一定满足条件。

检验一下不难得出![eq?n%5Cleq%204](https://latex.csdn.net/eq?n%5Cleq%204)是一定无法构造出来。

代码如下

```python
t = int(input())
for _ in range(t):
    n = int(input())
    if n<=4:
        print(-1)
    else:
        for i in range(1,n+1,2):
            if i!=5:
                print(i, end=' ')
        print(5, 4, end=' ')
        for i in range(2,n+1,2):
            if i!=4:
                print(i, end=' ')
        print()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# D. Sharky Surfing

**dificulty:1300**

**time limit per test:3 seconds**

**memory limit per test:256 megabytes**

[Problem - D - Codeforces](https://codeforces.com/contest/2037/problem/D)

## **原题**

Mualani loves surfing on her sharky surfboard!![05fa809e060c4a54839ac165d66ecef0.png](https://i-blog.csdnimg.cn/direct/05fa809e060c4a54839ac165d66ecef0.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

Mualani's surf path can be modeled by a number line. She starts at position 1, and the path ends at position L. When she is at position x with a jump power of k, she can jump to any **integer** position in the interval [x, x+k]. Initially, her jump power is 1.

However, her surf path isn't completely smooth. There are n hurdles on her path. Each hurdle is represented by an interval [l, r], meaning she cannot jump to any position in the interval [l, r].

There are also m power-ups at certain positions on the path. Power-up i is located at position ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24) and has a value of ![eq?%24v_i%24](https://latex.csdn.net/eq?%24v_i%24). When Mualani is at position ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24), she has the option to collect the power-up to increase her jump power by ![eq?%24v_i%24](https://latex.csdn.net/eq?%24v_i%24). There may be multiple power-ups at the same position. When she is at a position with some power-ups, she may choose to take or ignore each individual power-up. No power-up is in the interval of any hurdle.

What is the minimum number of power-ups she must collect to reach position L to finish the path? If it is not possible to finish the surf path, output -1.



玛拉妮喜欢在她的鲨鲨冲浪板上冲浪！

玛拉妮的冲浪路径可以用数轴来表示。她从位置 1 开始，路径在位置 L 结束。当她在位置 x ，跳跃能力为 k 时，她可以跳到区间 [x,x+k] 内的任何位置。最初，她的跳跃力量是 1 。

然而，她的冲浪之路并非一帆风顺。她的道路上有许多障碍。每个跨栏用一个区间 [l,r] 表示，这意味着她不能跳到区间 [l,r] 中的任何位置。

在路径的某些位置也有 m 力量提升。 力量提升 i 位于 ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24) 位置，值为 ![eq?%24v_i%24](https://latex.csdn.net/eq?%24v_i%24) 。当玛拉妮在位置 ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24) 时，她可以选择收集力量提升以增加她的跳跃能力 ![eq?%24v_i%24](https://latex.csdn.net/eq?%24v_i%24) 。在同一个位置可能会有多个升级道具。当她处于拥有一些力量提升的位置时，她可能会选择接受或忽略每个力量提升。在任何障碍的间隔中都没有力量提升。

她必须收集**多少个力量提升**才能到达位置 L 完成路径？如果无法完成冲浪路径，则输出 −1 。



**Input·**

The first line contains an integer ![eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29](https://latex.csdn.net/eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29) — the number of test cases.

The first line of each test case contains three integers n, m, and L ![eq?%281%20%5Cleq%20n%2C%20m%20%5Cleq%202%20%5Ccdot%2010%5E5%2C%203%20%5Cleq%20L%20%5Cleq%2010%5E9%29](https://latex.csdn.net/eq?%281%20%5Cleq%20n%2C%20m%20%5Cleq%202%20%5Ccdot%2010%5E5%2C%203%20%5Cleq%20L%20%5Cleq%2010%5E9%29)— the number of hurdles, the number of power-ups, and the position of the end.

The following n lines contain two integers ![eq?%24l_i%24](https://latex.csdn.net/eq?%24l_i%24) and ![eq?%24r_i%24](https://latex.csdn.net/eq?%24r_i%24) (![eq?%242%20%5Cleq%20l_i%20%5Cleq%20r_i%20%5Cleq%20L-1%24](https://latex.csdn.net/eq?%242%20%5Cleq%20l_i%20%5Cleq%20r_i%20%5Cleq%20L-1%24)) — the bounds of the interval for the i'th hurdle. It is guaranteed that ![eq?r_i%20&plus;%201%20%3C%20l_%7Bi&plus;1%7D](https://latex.csdn.net/eq?r_i%20&plus;%201%20%3C%20l_%7Bi&plus;1%7D) for all ![eq?%241%20%5Cleq%20i%20%3C%20n%24](https://latex.csdn.net/eq?%241%20%5Cleq%20i%20%3C%20n%24) (i.e. all hurdles are non-overlapping, sorted by increasing positions, and the end point of a previous hurdle is not consecutive with the start point of the next hurdle).

The following m lines contain two integers ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24) and ![eq?%24v_i%24](https://latex.csdn.net/eq?%24v_i%24) (![eq?%241%20%5Cleq%20x_i%2C%20v_i%20%5Cleq%20L%24](https://latex.csdn.net/eq?%241%20%5Cleq%20x_i%2C%20v_i%20%5Cleq%20L%24)) — the position and the value for the i'th power-up. There may be multiple power-ups with the same x. It is guaranteed that ![eq?%24x_i%20%5Cleq%20x_%7Bi&plus;1%7D%24](https://latex.csdn.net/eq?%24x_i%20%5Cleq%20x_%7Bi&plus;1%7D%24) for all ![eq?%241%20%5Cleq%20i%20%3C%20m%24](https://latex.csdn.net/eq?%241%20%5Cleq%20i%20%3C%20m%24)(i.e. the power-ups are sorted by non-decreasing position) and no power-up is in the interval of any hurdle.

It is guaranteed the sum of n and the sum of m over all test cases does not exceed ![eq?%242%20%5Ccdot%2010%5E5%24](https://latex.csdn.net/eq?%242%20%5Ccdot%2010%5E5%24)

.

第一行包含一个整数 ![eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29](https://latex.csdn.net/eq?t%20%281%20%5Cleq%20t%20%5Cleq%2010%5E4%29)—测试用例的数量。

每个测试用例的第一行包含三个整数 n 、 m 和 L ![eq?%281%20%5Cleq%20n%2C%20m%20%5Cleq%202%20%5Ccdot%2010%5E5%2C%203%20%5Cleq%20L%20%5Cleq%2010%5E9%29](https://latex.csdn.net/eq?%281%20%5Cleq%20n%2C%20m%20%5Cleq%202%20%5Ccdot%2010%5E5%2C%203%20%5Cleq%20L%20%5Cleq%2010%5E9%29)——栏数、升级次数和结束位置。

下面的 n 行包含两个整数 ![eq?%24l_i%24](https://latex.csdn.net/eq?%24l_i%24) 和 ![eq?%24r_i%24](https://latex.csdn.net/eq?%24r_i%24) (![eq?%242%20%5Cleq%20l_i%20%5Cleq%20r_i%20%5Cleq%20L-1%24](https://latex.csdn.net/eq?%242%20%5Cleq%20l_i%20%5Cleq%20r_i%20%5Cleq%20L-1%24) )—— i 的第一个跨栏的间隔边界。保证对所有的 ![eq?%241%20%5Cleq%20i%20%3C%20n%24](https://latex.csdn.net/eq?%241%20%5Cleq%20i%20%3C%20n%24)， ![eq?r_i%20&plus;%201%20%3C%20l_%7Bi&plus;1%7D](https://latex.csdn.net/eq?r_i%20&plus;%201%20%3C%20l_%7Bi&plus;1%7D) (即所有跨栏不重叠，按位置递增排序，前一个跨栏的终点与下一个跨栏的起点不连续)。

下面的 m 行包含两个整数 ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24) 和![eq?%24v_i%24](https://latex.csdn.net/eq?%24v_i%24)( ![eq?%241%20%5Cleq%20x_i%2C%20v_i%20%5Cleq%20L%24](https://latex.csdn.net/eq?%241%20%5Cleq%20x_i%2C%20v_i%20%5Cleq%20L%24) )-第 i 次力量提升的位置和值。可能有多个具有相同 x 的强化。保证对所有的 ![eq?%241%20%5Cleq%20i%20%3C%20m%24](https://latex.csdn.net/eq?%241%20%5Cleq%20i%20%3C%20m%24)，![eq?%24x_i%20%5Cleq%20x_%7Bi&plus;1%7D%24](https://latex.csdn.net/eq?%24x_i%20%5Cleq%20x_%7Bi&plus;1%7D%24)(即按不递减的位置排序)，且在任何障碍区间内不存在任何通电。

保证所有测试用例的 n和 m 之和不超过 ![eq?%242%20%5Ccdot%2010%5E5%24](https://latex.csdn.net/eq?%242%20%5Ccdot%2010%5E5%24)。



**Output**

For each test case, output the minimum number of power-ups she must collect to reach position L. If it is not possible, output −1.



对于每个测试用例，输出她必须收集到位置 L 的能量的最小数量。如果不可能，输出 −1 。

**Example**

Input

4
 2 5 50
 7 14
 30 40
 2 2
 3 1
 3 5
 18 2
 22 32
 4 3 50
 4 6
 15 18
 20 26
 34 38
 1 2
 8 2
 10 2
 1 4 17
 10 14
 1 6
 1 2
 1 2
 16 9
 1 2 10
 5 9
 2 3
 2 2


 OutPut

4
 -1
 1
 2
 



## 题解

首先考虑如何跨过某个障碍。

根据题意，玛拉妮不能在[l,r]的区间内，因此跨过障碍所需的最小的跳跃力量为r-l+2。

因为要使用最少的个数，在使用时应尽可能使用能量值高的，同时在使用时只要能量足够就不继续使用，这样能保证使用个数是最少的。

可以使用优先队列存储能量值。遍历障碍，将当前障碍左边未入队的提升的值入队。将队列中的最大值出队直到当前能量值足够越过当前障碍。如果队列为空是能量仍不够，则说明无法到达L，输出-1。

代码如下

```cpp
#include <iostream>
#include<queue>
using namespace std;
typedef long long ll;
 
inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
 
 
void solve(){
    ll n,m,l;
    n = read();
    m = read();
    l = read();
    ll lp[200009],rp[200009],xp[200009],val[200009];
    for (int i=0;i<n;i++){
        lp[i] = read();
        rp[i] = read();
    }
    for (int i=0;i<m;i++){
        xp[i] = read();
        val[i] = read();
    }
    priority_queue<ll> p;
    ll k=1,need,count=0,j=0;
    for (int i=0;i<n;i++){
        need =  rp[i] - lp[i] + 2;
        for(;j<m;j++){
            if(xp[j]<lp[i]){
                p.push(val[j]);
            }
            else{
            	break;
			}
        }
        while (!p.empty()&&k<need){
        	ll v = p.top();
            k += v;
            p.pop();
            count += 1;
        }
        if (p.empty()&&k<need){
            cout<<-1<<endl;
            return;
        }
    }
    cout<<count<<endl;
}
 
int main(){
    ll t = read();
    while (t--){
        solve();
    }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# E. Kachina's Favorite Binary String

**dificulty:1600**

**time limit per test:2 seconds**

**memory limit per test:256 megabytes**



[Problem - E - Codeforces](https://codeforces.com/contest/2037/problem/E)



![a552030a5f1c442983e0243a43023be3.png](https://i-blog.csdnimg.cn/direct/a552030a5f1c442983e0243a43023be3.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑



## 原题



This is an interactive problem.

Kachina challenges you to guess her favorite binary string* s of length n. She defines f(l, r) as the number of subsequences† of 01 in ![eq?%24s_l%20s_%7Bl&plus;1%7D%20%5Cldots%20s_r%24](https://latex.csdn.net/eq?%24s_l%20s_%7Bl&plus;1%7D%20%5Cldots%20s_r%24). **Two subsequences are considered different if they are formed by deleting characters from different positions in the original string, even if the resulting subsequences consist of the same characters.**

To determine s, you can ask her some questions. In each question, you can choose two indices l and r (![eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24](https://latex.csdn.net/eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24)) and ask her for the value of f(l, r).

Determine and output s after asking Kachina no more than n questions. However, it may be the case that s is impossible to be determined. In this case, you would need to report **IMPOSSIBLE** instead.

Formally, s is impossible to be determined if after asking n questions, there are always multiple possible strings for s, regardless of what questions are asked. **Note that if you report IMPOSSIBLE when there exists a sequence of at most n queries that will uniquely determine the binary string, you will get the Wrong Answer verdict.**



*A binary string only contains characters 0 and 1.

† A sequence a is a subsequence of a sequence b if a can be obtained from b by the deletion of several (possibly, zero or all) elements. For example, subsequences of 1011101 are 0, 1, 11111, 0111, but not 000 nor 11100.



这是一道交互题。

卡齐娜让你猜她最喜欢的长度为 n 的二进制字符串 ∗ s 。她将 f(l, r) 定义为 ![eq?%24s_l%20s_%7Bl&plus;1%7D%20%5Cldots%20s_r%24](https://latex.csdn.net/eq?%24s_l%20s_%7Bl&plus;1%7D%20%5Cldots%20s_r%24) 的子序列 † 01的个数。**如果两个子序列是通过删除原字符串中不同位置的字符而形成的，则认为它们是不同的，即使结果子序列由相同的字符组成。**

要确定 s ，你可以问她一些问题。在每个问题中，您可以选择两个索引 l 和 r ( ![eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24](https://latex.csdn.net/eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24) )，并询问她 f(l, r) 的值。

在向卡齐娜询问不超过 n 的问题后，确定并输出 s 。然而，可能是无法确定的情况。在这种情况下，您需要报告 **IMPOSSIBLE** 。

如果在问了n 个问题之后，无论问什么问题， s 总是有多个可能的字符串，那么 s 是不可能确定的。**请注意，如果您报告 IMPOSSIBLE，当存在最多 n查询序列时，将唯一地确定二进制字符串，你的回答将被判定为错误。**

\* 二进制字符串只包含字符0 和 1 。

† 如果 a 可以通过删除 b 中的几个(可能是零或全部)元素来获得，则序列 a 是序列 b$ 的子序列。例如， 1011101 的子序列是 0 ， 1 , 11111 , 0111 ，但 000 和 11100 不是。



**Input**

The first line of input contains a single integer t (![eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E3%24](https://latex.csdn.net/eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E3%24)) — the number of test cases.

The first line of each test case contains a single integer n (![eq?%242%20%5Cleq%20n%20%5Cleq%2010%5E4%24](https://latex.csdn.net/eq?%242%20%5Cleq%20n%20%5Cleq%2010%5E4%24)) — the length of s.

It is guaranteed that the sum of n over all test cases does not exceed ![eq?%2410%5E4%24](https://latex.csdn.net/eq?%2410%5E4%24)



第一行输入包含一个整数 t (![eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E3%24](https://latex.csdn.net/eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E3%24)) ——测试用例的数量。

每个测试用例的第一行包含一个整数 n (![eq?%242%20%5Cleq%20n%20%5Cleq%2010%5E4%24](https://latex.csdn.net/eq?%242%20%5Cleq%20n%20%5Cleq%2010%5E4%24)) ——长度为 s 。

保证所有测试用例 n 的和不超过 ![eq?%2410%5E4%24](https://latex.csdn.net/eq?%2410%5E4%24) 。



**Interaction**

To ask a question, output a line in the following format (do not include quotes)

\-  **"? l r"** (![eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24](https://latex.csdn.net/eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24))

The jury will return an integer f(l, r).

When you are ready to print the answer, output a single line in the following format

\-  If s is impossible to be determined, output **"! IMPOSSIBLE"**
 \-  Otherwise, output **"! s"**

After that, proceed to process the next test case or terminate the program if it was the last test case. Printing the answer does not count as a query.

The interactor is **not** adaptive, meaning that the answer is known before the participant asks the queries and doesn't depend on the queries asked by the participant.

If your program makes more than n queries for one test case, your program should immediately terminate to receive the verdict Wrong Answer. Otherwise, you can get an arbitrary verdict because your solution will continue to read from a closed stream.

After printing a query do not forget to output the end of line and flush the output. Otherwise, you may get Idleness limit exceeded verdict. To do this, use:

\-  fflush(stdout) or cout.flush() in C++;
 \-  System.out.flush() in Java;
 \-  flush(output) in Pascal;
 \-  stdout.flush() in Python;
 \-  see the documentation for other languages.



要问问题，以以下格式输出一行(不包括引号)

\-  **"? l r"** (![eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24](https://latex.csdn.net/eq?%241%20%5Cleq%20l%20%3C%20r%20%5Cleq%20n%24))

判题机将返回f(l, r) 的结果。

当您准备好打印答案时，以以下格式输出一行

—如果 s 无法确定，则输出 **"! IMPOSSIBLE"**。
 —否则，输出 **"! s"**。

在那之后，继续处理下一个测试用例，或者如果它是最后一个测试用例，则终止程序。打印答案不算作查询。

交互器不是自适应的，这意味着在参与者提出查询之前，答案是已知的，并且不依赖于参与者提出的查询。

如果您的程序对一个测试用例进行了超过 n 的查询，您的程序应该立即终止以收到错误答案的判决。否则，您可能会得到一个武断的结论，因为您的解决方案将继续从已关闭的输入流中读取数据。

打印查询后，不要忘记输出行尾并刷新输出。否则，你可能会得到超过闲置限制判决。要做到这一点，使用：

\- c++: fflush(stdout)或cout.flush()；
 \- Java: System.out.flush()；
 -Pascal: flush(output)；
 \- Python: stdout.flush()；
 -查看其他语言的文档。



**Example**

Input

2
 5

4

0

1

2

2

0



Output

? 1 5

? 2 4

? 4 5

? 3 5

! 01001

? 1 2

! IMPOSSIBLE



## 测评机

首先附上我自己写的本地测评机（使用时在main中写一段代码，输入输出使用input和print）

交互题的一大难点就是测试很麻烦（这个测评机前前后后改了三四个小时）

```python
'''
author:FZANOTFOUND
update_date:2024/11/20
version:1
'''


import sys
import time
import random
import traceback
from collections import deque

err = sys.stderr.write
stdout = sys.stdout


# 0 get t
# 1 get n
# 2 asking
state = 0 #current state
test_number = 0 #第几个测试
case_number = 0 #某个测试中第几次
res_que = deque() # 回答队列
ans_que = deque() # 用户答案队列
easy_mode = True
now_s = ''

def generate_random_numbers(t): # 生成某个测试的n
    numbers = []
    current_sum = max_sum_n + 1
    while current_sum > max_sum_n:
        current_sum = 0
        for _ in range(t):
            num = random.randint(2, max_sum_n//t) 
            current_sum += num
            numbers.append(num)
    return numbers

def generate_random_bitstring(n):
    if random.randint(1,100)<=round(impossible_probability*100):
        if random.randint(0,1):
            if random.randint(0,1):
                return '0' *n
            return '1' * n
        else:
            t = random.randint(0,n*2//3)
            return '1' * t + '0' * (n-t)
    else:
        return ''.join([str(random.randint(0,1)) for i in range(n)]) 
    
def Error(reason,error='', inCase=True):
    err(f"\n{reason} on test{test_number}" + (f" case{case_number}\n" if inCase else '\n'))
    if error:
        err(f"{error}")
    sys.exit()

def log(s, checker=False):
    if not checker and easy_mode:
        return
    stdout.write(str(s))
    stdout.write('\n')


def input(prompt='',/):
    global state, case_number, now_s
    if state == 0:
        state = 1
        ans = t
    elif state == 1:
        ans = n_data[case_number]
        state =2
        now_s = bit_strings[case_number]
        log(f'-------------------------\nbit_string of case{case_number}:{bit_strings[case_number]}')
    else:
        ans = res_que.popleft()
    return str(ans)

def print(*args, sep=' ',end = '\n',file=None, flush=None):
    global state,case_number
    req = ' '.join(map(str,args))
    if req.startswith('!'):
        log(f"user returned answer:{req.split()[1]}")
        ans_que.append(req.split()[1])
        state = 1
        case_number += 1
    elif req.startswith('?'):
        log(f"user asked {req}")
        try:
            a,b = map(int, req.split(' ')[1:3])
            if a>=b:
                WrongAnswer(f'Invaild print:{req}')
            res = f(a,b)
            log(f"machine return ans:{res}")
            res_que.append(res)
        except Exception as e:
            Error('Run Time Error:' ,str(e))
    else:
        Error('Run Time Error:' ,f'Invaild print:{req}')
        
def debug(*args, sep=' ',end = '\n',file=None, flush=None):
    if file is None:
        file = sys.stderr
    for i in args:
        file.write(str(i))
        file.write(sep)
    file.write(end)
    if flush:
        file.flush()

def f (a,b):
    number = 0
    total = 0
    for i in range(a-1,b):
        if now_s[i] == '0':
            number += 1
        else:
            total += number
    return total
 
def answer_check():
    log(f"\n============\nchecking test{test_number}",True)
    for i in range(len(bit_strings)):
        if not ans_que:
            Error('WrongAnswer',f"case{i}:Expect a string,found None",False)
        else:
            s = bit_strings[i]
            ans = 'IMPOSSIBLE' if  s.find('01')==-1 else s
            res = ans_que.popleft()
            if ans!=res:
               Error('WrongAnswer',f"case{i}:Expect {ans},found {res}",False)
            else:
                log(f"case{i} ok res:{res}"+('' if ans !='IMPOSSIBLE' else f'(origin:{s})'),True)
    log(f"\ntest{test_number} ok\n============\n",True)
                

class GetTraceBack:
    def __init__(self):
        self.errs = []
        
    def write(self, msg):
        self.errs.append(msg)
        
    def flush(self):
        pass

    def get(self):
        return self.errs

    def clear(self):
        self.errs = []

tracer = GetTraceBack()









#================================
# 修改以下几个变量修改测试数据范围
# 因为调小了默认数据范围（不然光log就能花很长时间），使用时长仅做参考
# !!!!为了方便debug，缩小了所有数据的范围
# 如果需要通过print进行调试，请将print改为debug,以免判题机给出RTE判定（可能与原来的print略有不同）
#获取输入input, 输出print
test_round = 50 # 测试轮数（数据为随机生成，为保证充分覆盖所有情况，不建议将test_round调的过小）
max_t = 20 # 对于一个test中,t的最大值
max_sum_n = 200 # n的和的最大值
impossible_probability = 0.2 # 生成的随机字符串中有多大概率最后答案为IMPOSSIBLE的概率,两位有效小数（不建议在作出本题前看生成IMPOSSIBLE case的代码）

def main():
    global easy_mode
    easy_mode = True
    # easy_mode =True 仅打印checker日志，中间的应答不打出 默认True
    # write your program here
    # @~@
    pass






#==================================================
#test code
test_t = test_round # 进行50次测试

log(f'test start,  round number {test_t}\n\n')
test_number = 0 # 第几个测试
for test_number in range(test_t):
    case_number = 0 # 某个测试中第几次
    log(f"test {test_number} start",True)
    t = random.randint(1,max_t)
    log(f"randomed t:{t}")
    log(f"generating {t} n(s)")
    n_data = generate_random_numbers(t)
    log(f"generating n bit-strings based on n_data")
    bit_strings = [generate_random_bitstring(n_data[j]) for j in range(t)]
    log(f"generate finish,main start")
    start_time = time.time()
    log(f"start_time:{start_time}",True)
    state=0
    try:
        main()
    except Exception as e:
        traceback.print_exc(file=tracer)
        errs = ''.join(tracer.get())
        Error('Run Time Error:' , errs)
        tracer.clear()
    end_time = time.time()
    log(f"end_time:{end_time}",True)
    log(f"using:{round((end_time-start_time)*1000)}ms",True) 
    answer_check()
log("\n==========================================\nAll test pass! congratulations!",True)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

使用测评机时，可以参照以下案例（~code~代表隐藏的代码块）

```python
~code~

def main():
    global easy_mode
    easy_mode = True
    # easy_mode =True 仅打印checker日志，中间的应答不打出 默认True
    # write your program here
    t = int(input()) # 获取输入
    ~code~
    print("? 1 2") # 询问
    debug(t) # 调试输出


~code~
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 题解

首先考虑以下情况

1.![eq?f%28l%2Cl&plus;1%29%20%3D%201](https://latex.csdn.net/eq?f%28l%2Cl&plus;1%29%20%3D%201) 则l,l+1一定为 01

2.![eq?f%28l%2Cl&plus;1%29%20%3D%200](https://latex.csdn.net/eq?f%28l%2Cl&plus;1%29%20%3D%200) 则l,l+1可能为 00,10,11中任何一种

3.![eq?%5Cforall%20r%20%5Cin%20%5Bl&plus;1%2Cr_0-1%5D%20f%28l%2Cr%29%20%3D%200](https://latex.csdn.net/eq?%5Cforall%20r%20%5Cin%20%5Bl&plus;1%2Cr_0-1%5D%20f%28l%2Cr%29%20%3D%200) 且 ![eq?f%28l%2Cr_0%29%20%3D%20k](https://latex.csdn.net/eq?f%28l%2Cr_0%29%20%3D%20k) 则 ![eq?l%20%5Crightarrow%20r_0%20-%20l%20&plus;%201%20-%20k](https://latex.csdn.net/eq?l%20%5Crightarrow%20r_0%20-%20l%20&plus;%201%20-%20k) 为 1 ![eq?r_0%20-%20k%20%5Crightarrow%20r_0%20-%201](https://latex.csdn.net/eq?r_0%20-%20k%20%5Crightarrow%20r_0%20-%201) 为 0 ,![eq?r_0](https://latex.csdn.net/eq?r_0)为1

4.按上述思路扫描完后，最后一个![eq?f%28l%2Cl&plus;1%29%20%3D%201](https://latex.csdn.net/eq?f%28l%2Cl&plus;1%29%20%3D%201) 且 ![eq?f%28l%2C%20n%29%20%3D%20k](https://latex.csdn.net/eq?f%28l%2C%20n%29%20%3D%20k)，则 ![eq?l%20&plus;%202%20%5Crightarrow%20l%20&plus;%201%20&plus;%20k](https://latex.csdn.net/eq?l%20&plus;%202%20%5Crightarrow%20l%20&plus;%201%20&plus;%20k) 为1，![eq?l%20&plus;%202%20&plus;%20k%20%5Crightarrow%20n](https://latex.csdn.net/eq?l%20&plus;%202%20&plus;%20k%20%5Crightarrow%20n) 为0

5.![eq?f%281%2Cn%29](https://latex.csdn.net/eq?f%281%2Cn%29)为0，则无法确定

按照这个思路写即可

代码如下

```python
t = int(input())
for _ in range(t):
    n = int(input())
    res = ''
    r = 2
    print(f"? 1 2")
    ans = int(input())        
    if ans==1:
        res += '01'
        r += 2
    else:
        r += 1
    while r<=n:
        print(f"? {len(res)+1} {r}")
        ans = int(input())
        if ans ==0 :
            r+=1
        else:
            res += '1' * (r - len(res) - ans - 1)
            res += '0' * ans
            res += '1'
            r = len(res) + 2
    if len(res)==0:
        print("! IMPOSSIBLE")
    elif len(res) != n:
        print(f"? {len(res)-1} {n}")
        ans = int(input())
        res += '1'*(ans-1)
        res += '0'*(n-len(res))
        print("!",res)
    else:
        print("!",res)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# F. Ardent Flames

**dificulty:2100**

**time limit per test: 4 seconds**

**memory limit per test: 256 megabytes**

[Problem - F - Codeforces](https://codeforces.com/contest/2037/problem/F)

![7507d8f39cc0472e8f4265ca9e42cdd7.png](https://i-blog.csdnimg.cn/direct/7507d8f39cc0472e8f4265ca9e42cdd7.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑

## 原题

You have obtained the new limited event character Xilonen. You decide to use her in combat.

There are n enemies in a line. The ![eq?i%27th](https://latex.csdn.net/eq?i%27th) enemy from the left has health ![eq?%24h_i%24](https://latex.csdn.net/eq?%24h_i%24) and is currently at position ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24). Xilonen has an attack damage of m, and you are ready to defeat the enemies with her.

Xilonen has a powerful "ground stomp" attack. **Before you perform any attacks**, you select an integer p and position Xilonen there (p can be any integer position, including a position with an enemy currently). Afterwards, for each attack, she deals m damage to an enemy at position p (if there are any), m-1 damage to enemies at positions p-1 and p+1, m-2 damage to enemies at positions p-2 and p+2, and so on. Enemies that are at least a distance of m away from Xilonen take no damage from attacks.

Formally, if there is an enemy at position x, she will deal ![eq?%24%5Cmax%280%2Cm%20-%20%7Cp%20-%20x%7C%29%24](https://latex.csdn.net/eq?%24%5Cmax%280%2Cm%20-%20%7Cp%20-%20x%7C%29%24) damage to that enemy each hit. **Note that you may not choose a different p for different attacks.**

Over all possible p, output the minimum number of attacks Xilonen must perform to defeat at least k enemies. If it is impossible to find a p such that eventually at least k enemies will be defeated, output -1 instead. Note that an enemy is considered to be defeated if its health reaches 0 or below.



你已经获得了新的限定角色希诺宁。你决定在战斗中使用她。

敌人排成一行。 第i个敌人的生命值为 ![eq?%24h_i%24](https://latex.csdn.net/eq?%24h_i%24) ，当前位置为 ![eq?%24x_i%24](https://latex.csdn.net/eq?%24x_i%24)。希诺宁的攻击伤害为 m ，你准备与她一起击败敌人。

希诺宁有一个强大的“踩地”攻击。**在你进行任何攻击之前，**你选择一个整数 p 并将希诺宁放置在那里( p 可以是任何整数位置，包括当前有敌人的位置)。之后，对于每次攻击，她对位置为 p 的敌人造成 m 伤害(如果有的话)，对位置为 p-1 和 p+1 的敌人造成 m-1 伤害，对位置为 p-2 和 p+2 的敌人造成 m-2 伤害，以此类推。距离希诺宁至少有一段距离的敌人不会受到攻击伤害。

正式地说，如果有一个敌人在 x 位置，她每次命中都会对该敌人造成 ![eq?%24%5Cmax%280%2Cm%20-%20%7Cp%20-%20x%7C%29%24](https://latex.csdn.net/eq?%24%5Cmax%280%2Cm%20-%20%7Cp%20-%20x%7C%29%24) 伤害。**请注意，您不能为不同的攻击选择不同的 p。**

在所有可能的 p 中，输出西洛宁必须执行的最少攻击次数以击败至少 k 个敌人。如果不可能找到一个 p 使最终至少 k 敌人被击败，则输出 -1 。注意，如果敌人的生命值达到或低于 0 ，则认为敌人已被击败。



**Input**

The first line contains an integer t (![eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E4%24](https://latex.csdn.net/eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E4%24)) – the number of test cases.

The first line of each test case contains three integers n, m, and k (![eq?%241%20%5Cleq%20k%20%5Cleq%20n%20%5Cleq%2010%5E5%24](https://latex.csdn.net/eq?%241%20%5Cleq%20k%20%5Cleq%20n%20%5Cleq%2010%5E5%24), ![eq?%241%20%5Cleq%20m%20%5Cleq%2010%5E9%24](https://latex.csdn.net/eq?%241%20%5Cleq%20m%20%5Cleq%2010%5E9%24)).

The following line contains n integers ![eq?%24h_1%2C%20h_2%2C%20...%2C%20h_n%24](https://latex.csdn.net/eq?%24h_1%2C%20h_2%2C%20...%2C%20h_n%24) (![eq?%241%20%5Cleq%20h_i%20%5Cleq%2010%5E9%24](https://latex.csdn.net/eq?%241%20%5Cleq%20h_i%20%5Cleq%2010%5E9%24)).

The last line of each testcase contains n integers ![eq?%24x_1%2C%20x_2%2C%20...%2C%20x_n%24](https://latex.csdn.net/eq?%24x_1%2C%20x_2%2C%20...%2C%20x_n%24) (![eq?%241%5Cleq%20x_i%20%5Cleq%2010%5E9%24](https://latex.csdn.net/eq?%241%5Cleq%20x_i%20%5Cleq%2010%5E9%24), ![eq?%24x_i%20%3C%20x_%7Bi&plus;1%7D%24](https://latex.csdn.net/eq?%24x_i%20%3C%20x_%7Bi&plus;1%7D%24) for all ![eq?%241%20%5Cleq%20i%20%3C%20n%24](https://latex.csdn.net/eq?%241%20%5Cleq%20i%20%3C%20n%24))

It is guaranteed that the sum of n over all test cases does not exceed ![eq?%2410%5E5%24](https://latex.csdn.net/eq?%2410%5E5%24).



第一行包含一个整数 t (![eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E4%24](https://latex.csdn.net/eq?%241%20%5Cleq%20t%20%5Cleq%2010%5E4%24))—测试用例的数量。

每个测试用例的第一行包含三个整数 n, m, 和 k (![eq?%241%20%5Cleq%20k%20%5Cleq%20n%20%5Cleq%2010%5E5%24](https://latex.csdn.net/eq?%241%20%5Cleq%20k%20%5Cleq%20n%20%5Cleq%2010%5E5%24), ![eq?%241%20%5Cleq%20m%20%5Cleq%2010%5E9%24](https://latex.csdn.net/eq?%241%20%5Cleq%20m%20%5Cleq%2010%5E9%24))。

下面一行包含 n 个整数 ![eq?%24h_1%2C%20h_2%2C%20...%2C%20h_n%24](https://latex.csdn.net/eq?%24h_1%2C%20h_2%2C%20...%2C%20h_n%24) (![eq?%241%20%5Cleq%20h_i%20%5Cleq%2010%5E9%24](https://latex.csdn.net/eq?%241%20%5Cleq%20h_i%20%5Cleq%2010%5E9%24))。

每个测试用例的最后一行包含 n 个整数![eq?%24x_1%2C%20x_2%2C%20...%2C%20x_n%24](https://latex.csdn.net/eq?%24x_1%2C%20x_2%2C%20...%2C%20x_n%24) (![eq?%241%5Cleq%20x_i%20%5Cleq%2010%5E9%24](https://latex.csdn.net/eq?%241%5Cleq%20x_i%20%5Cleq%2010%5E9%24), ![eq?%5Cforall%201%20%5Cleq%20i%20%3C%20n%2C%20x_i%20%3C%20x_%7Bi&plus;1%7D](https://latex.csdn.net/eq?%5Cforall%201%20%5Cleq%20i%20%3C%20n%2C%20x_i%20%3C%20x_%7Bi&plus;1%7D) ![eq?](https://latex.csdn.net/eq?))

保证所有测试用例 n 的和不超过 ![eq?%2410%5E5%24](https://latex.csdn.net/eq?%2410%5E5%24) 。



**Output**

For each test case, output an integer on a new line, the minimum number of attacks that must be performed to defeat at least k enemies. If it is impossible to find a p such that eventually at least k enemies will be defeated, output -1 instead.



对于每个测试用例，在新的一行上输出一个整数，这是必须执行的最少攻击次数，以击败至少 k 个敌人。如果不可能找到一个 p 使最终至少 k 敌人被击败，则输出 -1 。



**Example**

Input

6
 5 5 3
 7 7 7 7 7
 1 2 3 4 5
 9 5 9
 2 4 6 8 10 8 6 4 2
 1 2 3 4 5 6 7 8 9
 2 10 2
 1 1
 1 20
 2 10 1
 69696969 420420420
 1 20
 2 10 2
 10 15
 1 19
 2 2 2
 1000000000 1
 1 3
 

Output

2
 2
 -1
 6969697
 15
 1000000000
 

## 题解

这道题目并不在意p具体的位置，而是问具体的轮次，因此我们对轮次进行二分， 检查某个轮次后是否有k只怪物被杀死。

对于处在![eq?x_i](https://latex.csdn.net/eq?x_i)的怪物，要想将其在round轮内杀死，则每次攻击时收到的伤害至少为![eq?damage%20%3D%20%5Cleft%20%5Clfloor%20%7B%5Cfrac%7B%28h%5Bi%5D%20-%201%20&plus;%20round%29%7D%7Bround%7D%7D%20%5Cright%20%5Crfloor](https://latex.csdn.net/eq?damage%20%3D%20%5Cleft%20%5Clfloor%20%7B%5Cfrac%7B%28h%5Bi%5D%20-%201%20&plus;%20round%29%7D%7Bround%7D%7D%20%5Cright%20%5Crfloor)。

若这个数大于m，意味着无法将其在round轮内杀死。

若这个数小于等于于m ，则p在![eq?%5Bx%5Bi%5D%20-%20%28m%20-%20damage%29%2C%20x%5Bi%5D%20&plus;%20%28m%20-%20damage%29%5D](https://latex.csdn.net/eq?%5Bx%5Bi%5D%20-%20%28m%20-%20damage%29%2C%20x%5Bi%5D%20&plus;%20%28m%20-%20damage%29%5D)内能是处在![eq?x_i](https://latex.csdn.net/eq?x_i)的怪物死亡。我们只需检查是否有几个位置x在k个区间内（扫描线）。

注意扫描时处理入和出的顺序（例如我的代码要先出在入）

代码如下

```cpp
# include <iostream>
# include <vector> 
#include <algorithm>
#define ll long long
#define PLL pair<ll, ll>
using namespace std;
const ll inf = 1e18+9;
//const ll MOD = 998244353;

inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}

bool cmp(PLL x, PLL y){
    if (x.first != y.first) return x.first < y.first;
    else return x.second < y.second;
}

bool check(vector<ll> h, vector<ll> x, ll n,ll m,ll k, ll mid){
    // 检查是否有位置在 mid 次攻击后使得k只怪物死亡
    vector<PLL> d;
    for(int i=0;i<n;i++){
        
        /*
                m
             m-1 m-1 
          m-2       m-2
           
        */
        ll height = (h[i] - 1 + mid)/mid;
        if (height > m){
            continue;
        }
        d.push_back({(x[i] - m + height), 1});
        d.push_back({(x[i] + m - height + 1), -1});
    }
    sort(d.begin(), d.end(), cmp);
    ll count = 0;
    
    for(int i=0;i<d.size();i++){
        count += d[i].second;
        if (count >= k) return true;       
    }
    return false;

}

void solve(){
    ll n, m, k;
    n = read();
    m = read();
    k = read();
    vector<ll> h(n), x(n);
    for(int i=0;i<n;i++){
        h[i] = read();
    }
    for(int i=0;i<n;i++){
        x[i] = read();
    }
    ll l=1, r=inf;
    while (l <= r){
        ll mid = (l+r)>>1;
        if (check(h, x, n, m, k, mid)){
            r = mid - 1;
        }
        else{
            l = mid + 1;
        }
        //cout<<l << ' ' << r << endl;
    }
    cout<<((l>inf)?-1:l)<<endl;
}

int main(){
    ll t=read();
    while(t--){
        solve();
    }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



# G. Natlan Exploring

**dificulty:2000**

**time limit per test: 4 seconds**

**memory limit per test: 256 megabytes**

[Problem - G - Codeforces](https://codeforces.com/contest/2037/problem/G)

![ef93ac5905394cb0b870a527bb25f2b1.png](https://i-blog.csdnimg.cn/direct/ef93ac5905394cb0b870a527bb25f2b1.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)编辑



## 原题

You are exploring the stunning region of Natlan! This region consists of n cities, and each city is rated with an attractiveness ![eq?%24a_i%24](https://latex.csdn.net/eq?%24a_i%24). A directed edge exists from City i to City j if and only if ![eq?i%3Cj](https://latex.csdn.net/eq?i%3Cj) and ![eq?%5Cgcd%28a_i%2Ca_j%29%5Cneq%201](https://latex.csdn.net/eq?%5Cgcd%28a_i%2Ca_j%29%5Cneq%201), where ![eq?%24%5Cgcd%28x%2C%20y%29%24](https://latex.csdn.net/eq?%24%5Cgcd%28x%2C%20y%29%24) denotes the [[greatest common divisor (GCD)\]]() of integers x and y.

Starting from City 1, your task is to determine the total number of distinct paths you can take to reach City n, modulo ![eq?%24998%5C%2C244%5C%2C353%24](https://latex.csdn.net/eq?%24998%5C%2C244%5C%2C353%24). Two paths are different if and only if the set of cities visited is different.



你正在探索令人惊叹的纳塔地区！该区域由 n 个城市组成，每个城市都具有吸引力 ![eq?%24a_i%24](https://latex.csdn.net/eq?%24a_i%24) 。当且仅当 ![eq?i%3Cj](https://latex.csdn.net/eq?i%3Cj) 且 ![eq?%5Cgcd%28a_i%2Ca_j%29%5Cneq%201](https://latex.csdn.net/eq?%5Cgcd%28a_i%2Ca_j%29%5Cneq%201) 存在一条从City i 到City j 的有向边，其中 ![eq?%24%5Cgcd%28x%2C%20y%29%24](https://latex.csdn.net/eq?%24%5Cgcd%28x%2C%20y%29%24) 表示整数 x 和 y的[[最大公约数\]](https://baike.baidu.com/item/最大公约数/869308?fr=ge_ala)。

从城市 1开始，你的任务是确定到达城市 n 的不同路径的总数，对 ![eq?%24998%5C%2C244%5C%2C353%24](https://latex.csdn.net/eq?%24998%5C%2C244%5C%2C353%24) 取模。当且仅当所访问的城市集合不同时，两条路径是不同的。



**Input**

The first line contains an integer n (![eq?%242%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%24](https://latex.csdn.net/eq?%242%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%24)) — the number of cities.

The second line contains n integers ![eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24](https://latex.csdn.net/eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24) (![eq?%242%20%5Cleq%20a_i%20%5Cleq%2010%5E6%24](https://latex.csdn.net/eq?%242%20%5Cleq%20a_i%20%5Cleq%2010%5E6%24)) — the attractiveness of each city.



第一行包含一个整数 n (![eq?%242%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%24](https://latex.csdn.net/eq?%242%20%5Cleq%20n%20%5Cleq%202%20%5Ccdot%2010%5E5%24)) —城市的数量。

第二行包含 n个整数 ![eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24](https://latex.csdn.net/eq?%24a_1%2C%20a_2%2C%20%5Cldots%2C%20a_n%24) (![eq?%242%20%5Cleq%20a_i%20%5Cleq%2010%5E6%24](https://latex.csdn.net/eq?%242%20%5Cleq%20a_i%20%5Cleq%2010%5E6%24)) ——每个城市的吸引力。



**Output** 

Output the total number of distinct paths you can take to reach City n, modulo ![eq?%24998%5C%2C244%5C%2C353%24](https://latex.csdn.net/eq?%24998%5C%2C244%5C%2C353%24).



输出到达City n 的不同路径的总数，对 ![eq?%24998%5C%2C244%5C%2C353%24](https://latex.csdn.net/eq?%24998%5C%2C244%5C%2C353%24) 取模。



## 题解

假设我们已经知道了所有有向边，不难得出 ：令dp[i]为1->i的路径数， ![eq?dp%5Bi%5D%20%3D%20%5Csum%20%28dp%5Bj%5D%29](https://latex.csdn.net/eq?dp%5Bi%5D%20%3D%20%5Csum%20%28dp%5Bj%5D%29) ![eq?%2C%20i%5Crightarrow%20j](https://latex.csdn.net/eq?%2C%20i%5Crightarrow%20j)为一条有向边。

放到这道题即为 ![eq?dp%5Bi%5D%20%3D%20%5Csum_%7Bj%3D1%7D%5E%7Bi-1%7D%20dp%5Bj%5D%20%28%5Cgcd%20%28a%5Bi%5D%2C%20a%5Bj%5D%29%5Cneq1%29](https://latex.csdn.net/eq?dp%5Bi%5D%20%3D%20%5Csum_%7Bj%3D1%7D%5E%7Bi-1%7D%20dp%5Bj%5D%20%28%5Cgcd%20%28a%5Bi%5D%2C%20a%5Bj%5D%29%5Cneq1%29)

但是这种方法的时间复杂度为![eq?O%28n%5E2%29](https://latex.csdn.net/eq?O%28n%5E2%29) ,而这道题 n的范围达到了![eq?10%5E6](https://latex.csdn.net/eq?10%5E6)，必定会超时

关注![eq?%5Cgcd%20%28a%5Bi%5D%2C%20a%5Bj%5D%29](https://latex.csdn.net/eq?%5Cgcd%20%28a%5Bi%5D%2C%20a%5Bj%5D%29)，其结果的种类并不多（2,3,5,7,11...及其乘积）

定义s[i] 为 ![eq?s%5Bi%5D%20%3D%20%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20dp%5Bj%5D%20%28a%5Bj%5D%20%5C%25i%3D%3D0%29](https://latex.csdn.net/eq?s%5Bi%5D%20%3D%20%5Csum_%7Bj%3D1%7D%5E%7Bn%7D%20dp%5Bj%5D%20%28a%5Bj%5D%20%5C%25i%3D%3D0%29)，则在计算新的dp[i]时只需加上所有的因子的对应的s就行。

注意到![eq?gcd%286%2C%2012%29%20%3D%206%20%3D%202%5Ctimes%203](https://latex.csdn.net/eq?gcd%286%2C%2012%29%20%3D%206%20%3D%202%5Ctimes%203) 因此 在计算 有多个质因子的数时使用容斥原理 （例如此处应为![eq?s%5B2%5D%20&plus;%20s%5B3%5D%20-%20s%5B6%5D](https://latex.csdn.net/eq?s%5B2%5D%20&plus;%20s%5B3%5D%20-%20s%5B6%5D)）

 为了压缩质因数分解的时间，我们可以提前用质数筛求出（![eq?1%20%5Crightarrow%2010%5E6](https://latex.csdn.net/eq?1%20%5Crightarrow%2010%5E6)）所有的数的最小质因子，

在求某个数的质因子时只需读取当前的最小质因子并除以它即可



代码如下

```cpp
# include <iostream>
# include <vector> 
#define ll long long
#define PII pair<ll, ll>
using namespace std;
const ll inf = 1e18+9;
const ll MOD = 998244353;
 
inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
 
void printvec(vector<ll> vec) { 
    for (auto it = vec.begin(); it != vec.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;
}
 
ll sign(ll x){
    if (__builtin_popcount(x) % 2 == 0) return -1;
    else return 1;
}
 
ll maxN = 1000000;
int main(){
    ll n = read();
    vector<ll> a(n+1,0);
    for(int i=1;i<=n;i++){
        a[i] = read();
    }
    // 质数筛 d[i] 为 i 的最小质因子
	vector<ll> d(maxN+1, 0);
    for (int i = 0; i <= maxN; i++) d[i] = i;
    for (int i = 2; i*i <= maxN; i++) {
        if (d[i] == i) {// 没有被更改过
            for (ll j = i*i; j <=maxN; j+=i) {
                d[j] = i;
            }
        }
    }
    vector<ll> dp(n+1, 0);// dp[i] 1 -> i 的路径数
    dp[1] = 1; // 1 -> 1 1条
    vector<ll> s(maxN+1, 0);// s[i] sum([dp[j]  if a[i] % j == 0 for j in range(1, n+1)])
    vector<ll> factor;
    for(int i=1;i<=n;i++){
        factor.clear();
        ll num = a[i];
        //利用质数筛进行质因数分解
        while(num>1){
            ll tfactor = d[num];
            while(num%tfactor==0){
                num /= tfactor;
            }
            factor.push_back(tfactor);
        }
        for (int j=1;j< (1<<factor.size());j++){// 容斥原理
            ll t = 1;
            for(ll k=0;k<factor.size();k++){
                if (j>>k&1){
                    t *= factor[k];
                }
            }
            dp[i] = (dp[i] + s[t] * sign(j) + MOD)%MOD;
        }
 
        for (int j=1;j< (1<<factor.size());j++){// 注意s[i]的定义， 更新s
            ll t = 1;
            for(ll k=0;k<factor.size();k++){
                if (j>>k&1){
                    t *= factor[k];
                }
            }
            s[t] = (s[t] + dp[i] + MOD)%MOD;
        }
    }
    cout << dp[n] <<endl;
 
    return 0;
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

# 图片链接

https://codeforces.com/predownloaded/b1/f4/b1f460f3b3dc0a21b417aece154d333df202f737.png

A:[为你，千千万万张。——留影叙佳期·基尼奇篇_手机游戏热门视频](https://www.bilibili.com/video/BV1WimrYjEKb/?spm_id_from=333.337.search-card.all.click&vd_source=f1214fdbab38e700acb7228742397196)



B:[原神的动态 - 哔哩哔哩](https://www.bilibili.com/opus/1003692685537574918?spm_id_from=333.1365.0.0)


 D: https://i0.hdslb.com/bfs/archive/228c5f0dff904bac8c0ff9b6e3c512487d6bdfc0.jpg



E:[宝宝，你是一只香软芝士小蛋糕❤【卡齐娜/原摄】_原神](https://www.bilibili.com/video/BV1uXnReUE2f/)https://i0.hdslb.com/bfs/new_dyn/8a8f67351bc9d136451f50d2ad2a484e271961968.png



F:[【希诺宁】摆 拍 狂 魔 PLUS_手机游戏热门视频](https://www.bilibili.com/video/BV1Tt22YPEYD/?spm_id_from=333.337)



G:[纳塔狂飙小队，出征！_原神](https://www.bilibili.com/video/BV1g8SqYQE5H/?spm_id_from=333.337)

https://i0.hdslb.com/bfs/archive/596f5b57ce6508d1d9565d6a1d6b50fd8a02b62a.jpg