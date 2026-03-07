# A. ICPC Regionals

按题意判断即可。

注意 $ \lceil \frac{n}{10} \rceil$ 可以用 $\lfloor \frac{n+9}{10} \rfloor$ 计算。

时间复杂度 $O(1)$。

```python
n, k = map(int, input().split())
t = (n+9)//10
if k <= t:
    print("Gold Medal")
elif k <= 3*t:
    print("Silver Medal")
elif k <= 6*t:
    print("Bronze Medal")
else:
    print("Da Tie")
```



# B.Card Game

不难发现，把把牌合并要不一张都不和，此时为原来的最大值，要不就全部和，此时为 $n$。

答案即为 $max(n, max(a))$。

时间复杂度 $O(n)$。

```python
for _ in range(int(input())):
    n = int(input())
    a = list(map(int, input().split()))
    print(max(max(a), n))
```



# C. Palindrome Coloring

如果原来就是一个回文串，则答案为 $1$。

否则我们可以先选择所有的 $0$，再选择所有的 $1$，两个子序列一定是回文串，答案为 $2$。

时间复杂度 $O(n)$。

```python
for _ in range(int(input())):
    s = input().strip()
    if s[::-1] == s:
        print(1)
    else:
        print(2)
```



# D.Digital Pairing

题意即为选择 $n$ 个数字，使其按位与最大。

已知答案为 $x$，则一定有至少 $n$ 个数字 $a_i$ 满足 $x\& a_i = x$。

不难想到可以从大到小按位枚举，如果当前答案存在至少 $n$ 个满足 $x\& a_i = x$，则可以更新答案。

时间复杂度 $O(n loga_i)$。

```python
for _ in range(int(input())):
    n = int(input())
    a = [0] + list(map(int, input().split()))
    ans = 0
    for i in range(60, -1, -1):
        now = ans | (1<<i)
        cnt = 0
        for j in range(1, 2*n+1):
            if (a[j] & now) == now:
                cnt += 1
        if cnt >= n:
            ans = now
    print(ans)
```



# E.Beautiful Sequence

不难想到枚举 gcd，使用容斥处理。

如果没有数组的 ⁡gcd 不存在于数组中的条件，我们只需要从打到小枚举 gcd，则所有是当前 gcd 倍数的数字，任选其中的一部分的 gcd 是枚举的 gcd 或者其倍数。

我们只需要减去是当前枚举的 gcd 的倍数的情况就能得出答案。

回到本题，不难想到我们只需要在统计单的时候，减去包含的枚举的 gcd 这个数字的情况即可。

时间复杂度 $O(n ln n)$。

```python
from collections import Counter
MOD = 998244353
for _ in range(int(input())):
    n = int(input())
    a = list(map(int, input().split()))
    memo = Counter(a)
    cnt = [0 for i in range(n+1)]
    for i in range(1, n+1):
        for j in range(i, n+1, i):
            cnt[i] += memo[j]
    ans = 0
    res = [0 for i in range(n+1)] # res 即为 gcd 为 d 的子序列个数（没有限制条件）
    for i in range(n, 0, -1):
        t = cnt[i] - memo[i]
        tot = (pow(2, t, MOD) - 1)%MOD
        for j in range(2*i, n+1, i):
            tot = (tot - res[j] + MOD)%MOD
        tot2 = (pow(2, cnt[i], MOD) - 1)%MOD
        for j in range(2*i, n+1, i):
            tot2 = (tot2 - res[j] + MOD)%MOD
        res[i] = tot2
        ans = (ans + tot)%MOD
    print(ans)
```



# F.Bracket Counting

~~经典状压 dp（~~

首先不难发现，所有字符串中的左右括号数量之和必须相等。

一个字符串要能够接到现在的字符串上去，当期仅当对于任意位置，右括号的数量小于左括号的数量。

所以，我们处理每个字符串余下的没有匹配的括号的数量 $k$，以及右括号比左括号少的最多的数量 $t$。

状压 dp 时，如果当前的字符串的 $k$ 不小于当前的枚举的字符串 $t$ ，则我们可以把字符串拼接上去，否则不能。

时间复杂度 $O(n \times 2^n)$。

 ```python
 MOD = 10**9 + 7
 for _ in range(int(input())):
     n = int(input())
     ss = [input() for i in range(n)]
     
     k = [0 for i in range(n)]
     t = [0 for i in range(n)]
     tot = 0
     for i in range(n):
         s = ss[i]
         now = 0
         mi = 10**9
         for ch in s:
             if ch == '(':
                 now += 1
             else:
                 now -= 1
             mi = min(now, mi)
         k[i] = now
         t[i] = max(0, -mi)
         tot += now
             
     if tot != 0:
         print(0)
         continue
     
     su = [0 for i in range(1<<n)]
     dp = [0 for i in range(1<<n)]
     dp[0] = 1
     for mask in range(1, 1<<n):
         for i in range(n):
             if mask >>i & 1:
                 su[mask] += k[i]
     for mask in range(1<<n):
         if dp[mask] == 0:
             continue
         now = su[mask]
         for j in range(n):
             if mask >> j & 1 or now < t[j]:
                 continue
             dp[mask|(1<<j)] = (dp[mask|(1<<j)] + dp[mask])%MOD
     print(dp[(1<<n)-1]%MOD)
 ```
