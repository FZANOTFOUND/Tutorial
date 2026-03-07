# A.小红的好01串

显然有且仅有以 $1$ 开头的和以 $0$ 开头的两种。

所以答案为 $2$。

```py
print(2)
```



# B. 小红的01串距离

按题意模拟即可。

```py
for _ in range(int(input())):
    n = int(input())
    s = input()
    a = []
    for i in range(n):
        if s[i] == '1':
            a.append(i)
    print("Yes" if(a[0]+a[2]==2*a[1]) else "No")
```



# C.小红的好01串修改

由 $A$ 可知有 $1$ 开头的和以 $0$ 开头的两种。

枚举两种从左往右修改一遍取最小。如果不能则输出 $-1$。

```py
def cal(s, fi):
    t = fi
    cnt = 0
    for i in range(len(s) - 1):
        if s[i] != fi:
            s[i] ^= 1
            s[i+1] ^= 1
            cnt += 1
        fi ^= 1
    for i in range(len(s)):
        if s[i] != t:
            return 10**18
        t ^= 1
    return cnt


for _ in range(int(input())):
    n = int(input())
    s = list(map(int, list(input())))
    mi = min(cal(s[:], 0), cal(s[:], 1))
    print(mi if mi < 10**18 else -1)
```



# D.小红的华撃串

手玩一下可知最终的字符串一定形如 $0101$ 或者 $1010$。（每个字符可以有多个，例如$00001000011$)

本题 $4 \le n \le 500$ ，$O(n^3)$ 枚举无法通过。

考虑 $dp$ ，令 $dp[i][j][k]$ 为 第 $i$ 个位置及之前共分了 $j$ 段，以 $k$ 结尾的最小操作次数。（$1\le i\le n$，$1\le j \le 4$，$0\le k \le 1$）

对于 $i$ 位置，若在 $i$ 之前新分割一段，有 $dp[i][j][k] = min(dp[i][j][k], dp[i-1][j-1][k\oplus 1] + [s[i]!= k])$ （$i > 1$）

若不分割，有 $dp[i][j][k] = min(dp[i][j][k], dp[i-1][j][k] + [s[i]!=k])$ 

最终答案为 $min(dp[i][4][0],dp[i][4][1])$

时间复杂度 $O(4*2*n)$

```py
n = int(input())
s = [0] + list(input())
mi = 10**18
dp = [[[mi, mi] for i in range(5)] for i in range(n+1)]
dp[1][1][0] = int(s[1] != '0')
dp[1][1][1] = int(s[1] != '1')
for i in range(2, n+1):
    for j in range(1, 5):
        for k in range(2):
            dp[i][j][k] = min(dp[i][j][k], dp[i-1][j][k]+(s[i]!=str(k)))
            if j > 1:
                dp[i][j][k] = min(dp[i][j][k],dp[i-1][j-1][k^1]+(s[i]!=str(k)))
print(min(dp[n][4]))
```



# E/F 小红的01串

对于一段极长连续的 $1$ 串，其的贡献为 $\frac{l*(l+1)}{2}$。

要让长度最小，考虑 [完全背包](https://oi-wiki.org/dp/knapsack)    。

令 $w_i = \frac{i*(i+1)}{2}, c_i = i + 1$ 。（质量包括用于分割的 $0$）

则 $E$ 只需求出凑出 $k$ 的最小质量。

$F$ 在 $E$ 的基础上加一个回溯求最小质量的方案即可。

时间复杂度 $O(k*\sqrt{2*k})$

##  预处理

```py

from bisect import bisect_left, bisect_right
mxn = 640
w = [i*(i+1)//2 for i in range(mxn+1)]
c = [i + 1 for i in range(mxn+1)]
assert(w[-1]>(2*10**5+7))
dp = [10**18 for i in range(2*10**5+1)]
dp[0] = 0
pre = [-1 for i in range(2*10**5+1)]
for l in range(1, mxn+1):
    for x in range(w[l], 2*10**5+1):
        if dp[x-w[l]] + c[l] < dp[x]:
            dp[x] = dp[x - w[l]] + c[l]
            pre[x] = l
```

## E

```CPP
for _ in range(int(input())):
    k = int(input())
    print(dp[k]-1)
```

## F

```py
for _ in range(int(input())):
    k = int(input())
    res = []
    cur = k
    while cur > 0:
        l = pre[cur]
        res.append(l)
        cur -= w[l]
    res = res[::-1]
    print('1'*res[0], end='')
    for i in res[1:]:
        print('0',end='')
        print('1'*i,end='')
    print()
```



# G. 小红的双排列查询

想到以下条件即可：

1. $r-l+1$ 必须为 $2$ 的倍数且所有的数字两两匹配。（用随机数+前缀异或和判断）

2. $\max_{i = l}^{r} = \frac{r-l+1}{2}$。（用 st 表或者线段树判断）
3. $\sum_{i = l}^{r}  a_i = \max_{i = l}^{r}*(\max_{i = l}^{r}+1)  $。（用前缀和判断）

按上述判断一遍即可。

时间复杂度约为 $O(4n + nlogn + q)$


**upd**

有hack样例 （$\texttt{1 1 3 3 3 3 3 3 5 5}$），还需要判断  $\sum_{i = l}^{r}  a_i^2 = \frac{mx*(mx+1)*(2*mx+1)}{3}  $

实际上多判断几个 $a_i^k$ 之和就不会被 hack 了。（

```cpp
mt19937_64 rng(chrono::steady_clock::now().time_since_epoch().count());//rng()

ull m[200005];
void solve(){
    ll n = read(), q = read();
    vector<ull> a(n+1), pre(n+1), presum(n+1), presum2(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    for(ll i=1;i<=n;i++) pre[i] = pre[i-1] ^ m[a[i]];
    for(ll i=1;i<=n;i++) presum[i] = presum[i-1] + a[i];
    for(ll i=1;i<=n;i++) presum2[i] = presum2[i-1] + a[i]*a[i];
    ll p = __lg(n) + 10;
    vector<vector<ull>> st(p+1, vector<ull>(n+1));
    for(ll i=1;i<=n;i++) st[0][i] = a[i];
    for(ll k=1;k<=p;k++){
        for(ll i=1;i+((1<<k)-1)<=n;i++){
            st[k][i] = max(st[k-1][i], st[k-1][i+(1<<(k-1))]);
        }
    }
    function<ull(ull, ull)> query = [&](ull l, ull r){
        ll k = __lg(r-l+1);
        return max(st[k][l], st[k][r-(1<<k)+1]);
    };
    while(q--){
        ll l = read(), r = read();
        if((r-l+1)&1){
            puts("No");
            continue;
        }
        ull val1 = pre[r]^pre[l-1];
        ull val2 = query(l, r);
        ull val3 = presum[r]-presum[l-1];
        ull val4 = presum2[r] - presum2[l-1];
        ull mx = (r-l+1)/2;
        if(val1 ==0 && val2==mx &&val3 == (1+mx)*mx && val4 == (mx)*(mx+1)*(2*mx+1)/3){
            puts("Yes");
        }
        else{
            puts("No");
        }
    }
}
 
int main(){
    for(ll i=1;i<=200000;i++) m[i] = rng();
    ll t = 1;
    while(t--){
        solve();
    }
}
```