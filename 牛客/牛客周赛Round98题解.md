~~本来想30min速通的，结果F题取模一开始取成1e9+7，后面又爆ll，没能速通成功。~~

# A.小红与奇数

暴力遍历所有因子，检查是否有一组满足条件。

```python
x = int(input())
f = 0
for i in range(1, x+1):
    if x % i == 0 and (x + i) % 2 == 1:
        f = 1
print("Yes" if f else "No")
```

[A题代码](https://ac.nowcoder.com/acm/contest/view-submission?submissionId=78002882)



# B.小红与gcd三角形

算出三条边的值，检查最小的两条边之和是否大于第三边即可。

```py
from math import gcd
t = int(input())
for _ in range(t):
    x, y = map(int, input().split())
    a = sorted([x, y, gcd(x, y)])
    print('Yes' if a[0] + a[1] > a[2] else 'No')
```

[B题代码](https://ac.nowcoder.com/acm/contest/view-submission?submissionId=78002959)



# C.小红与red

遍历一遍字符串，遇到相邻相同的，为了使操作次数最小，我们需要将其改为和两侧均不同的字符。

```py
n = int(input())
s = list(input())
s.append('@')
def other(a, b):
    t = ['r', 'e', 'd']
    for ch in t:
        if ch != a and ch != b:
            return ch
for i in range(1, n):
    if s[i] == s[i-1]:
        s[i] = other(s[i-1], s[i+1])
print(''.join(s[:n]))
```

[C题代码](https://ac.nowcoder.com/acm/contest/view-submission?submissionId=78003114)



# D.小红与好数组

dfs搜索所有的数组

```python
n = int(input())

res = []

def dfs(left, now):
    if left == 0:
        res.append(now[:])
        return         
    for i in range(1, left+1):
        if not now or i != now[-1]:
            dfs(left - i, now + [i])
dfs(n, [])
res.sort()
for j in res:
    print(*j)
```

[D题代码](https://ac.nowcoder.com/acm/contest/view-submission?submissionId=78003312)



# E.小红与gcd和sum

我们知道 $gcd(a, a*b)$ = $a$($a$, $b$为正整数)。

因此想到可以枚举 $gcd$, 统计数组中为 $gcd$ 的倍数的所有数之和，在乘上 $gcd$。（前提是数组中有值为gcd的数）

所有的结果取最大即可。

注意由于 $\sum \limits_{1}^{n} \frac{1}{n} \rightarrow ln(n)$，时间复杂度约为 $n*ln(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1);
    map<ll, ll> memo;
    for(ll i=1;i<=n;i++){
        a[i] = read();
        memo[a[i]]++;
    }
    ll ans = 0;
    for(ll i=1;i<=maxn;i++){
        if(!memo[i]) continue;
        ll val = 0;
        for(ll j=i;j<=maxn;j+=i){
            val += memo[j] * j;
        }
        ans = max(val * i, ans);
    }
    print(ans);
}
```

[E题代码](https://ac.nowcoder.com/acm/contest/view-submission?submissionId=78003643)



# F.小红与天使猫猫酱

打表可得 $22^x$ 有 $(x+1)^2$ 个因子。

（证明的话例如$22$ 有 $1$, $2$, $11$, $22$。 $22^2$的因子可以由 $22$ 的因子相乘得到，但是$2*11 = 1*22$ 要去重。数学归纳可证上述结论）

于是 $b_i$ = $(\frac{2}{9} * (10^i - 1) + 1)^2$ = $\frac{4}{81} * 100^i + \frac{28}{81} * 10^i  + \frac{49}{81}$

求和得到 $\sum \limits_{i=1}^{n} b_i = \frac{4}{81} * 100 * \frac{100^n -1}{100-1} + \frac{28}{81} * 10 * \frac{10^n -1}{10-1}  + \frac{49}{81} * n$

注意$49*81^{MOD-2} \%MOD  * n \%MOD$会爆 $ll$ ,要写成$49*81^{MOD-2} \%MOD  * (n \%MOD) \%MOD$（警钟敲烂）

```cpp
void solve(){
    ll n = read();
    ll tt1 = (400%MOD * ksm(99 * 81%MOD, MOD-2)%MOD)%MOD*(ksm(100, n)%MOD + MOD- 1 )%MOD; 
    ll tt2 = (280%MOD * ksm(9 * 81%MOD, MOD-2)%MOD)%MOD * (ksm(10, n)%MOD - 1 + MOD)%MOD;
    ll tt3 = (49 * ksm(81, MOD-2)%MOD)%MOD*(n%MOD)%MOD;
    print(((tt1%MOD + tt2%MOD)%MOD + tt3)%MOD);
}
```

[F题代码](https://ac.nowcoder.com/acm/contest/view-submission?submissionId=78005479)