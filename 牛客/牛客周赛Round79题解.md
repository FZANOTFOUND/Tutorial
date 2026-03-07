# 牛客周赛 Round 79 题解（A-F）

# A.小红的合数寻找


我们知道除了 $2$ 以外的偶数均为质数，因此 $x > 1$ 时 $2*x$ 一定为合数。

$x = 1$ 时显然无解

```python
x = int(input())
print(2*x if x!=1 else -1)
```


# B.小红的小球染色


不难想到，我们无间隔的选择白色小球，此时为最大值。

由于如果有两个连续的不会结束，因此我们选择的一定只能间隔一个。

当 $n\mod 3 = 2$时，间隔一个选择后会剩下一组白色小球，仍会被选择。

```python
n = int(input())
print(n//3 + (n%3 == 2), n//2)
```



# C.小红的二叉树

简称长度为 $2$ 的简单路径为 $2$ 路径

对每个节点，若其下方至少有两层，则以该节点为起点的 $2$ 路径有 $4$  条。(图一）

同时，若该节点不为叶子结点，则有一条从左节点经过该节点到到右节点的 $2$ 路径。（图二）




![C1](https://uploadfiles.nowcoder.com/images/20250202/226800108_1738503266542/5CE3B6C6E5302382B174F6D9A0F20034)
![C2](https://uploadfiles.nowcoder.com/images/20250202/226800108_1738503351569/24D9A24B8C1DA5AFE0132A45C2084D0D)


```python
n = int(input())
ans = 0
pre = 1
for i in range(1, n):
    if n - i >= 2:
        ans =(ans + 4 * pre)%(10**9+7)
    ans = (ans + pre)%(10**9+7)
    pre = (pre * 2)%(10**9+7)# 每一层节点数翻倍
print(ans%(10**9+7))
```

# D.小红的“质数”寻找

若 $x$ 开头为 $1$ ,则 $2000...0$（长度和 $x$ 相同) 一定在 $[x, 2 \times x]$ 区间内。

若 $x$ 开头为 $2$ ,则 $3000...0$（长度和 $x$ 相同) 一定在 $[x, 2 \times x]$ 区间内。

若 $x$ 开头为 $3$ 或 $4$ ,则 $5000...0$（长度和 $x$ 相同) 一定在 $[x, 2 \times x]$ 区间内。

若 $x$ 开头大于等于 $6$ ,则 $11000...0$（长度比 $x$ 大一位) 一定在 $[x, 2 \times x]$ 区间内。

若 $x$ 开头为 $5$ ，当 $x$ 为 $50...0$ 时，本身满足条件；当$x$ 不为 $50...0$ 时，则 $1000...01$（长度比 $x$ 大一位) 一定在 $[x, 2 \times x]$ 区间内。

```python
t = int(input())
for _ in range(t):
    x = input()
    if  int(x[0]) > 5:
        print('11' + '0'*(len(x)-1))
    elif int(x[0]) == 5:
        if x == '5':
            print('5')
        elif x[0] == '5' and all([i=='0' for i in x[1:]]):
            print(x)
        else:
            print('1'+'0'*(len(x)-1) + '1')
    elif int(x[0]) == 4:
        print('5' + '0'*(len(x)-1))
    elif int(x[0]) == 3:
        print('5' + '0'*(len(x)-1))
    elif int(x[0]) == 2:
        print('3' + '0'*(len(x)-1))
    elif int(x[0]) == 1:
        print('2' + '0'*(len(x)-1))
```



# E.小红的好排列

当 $i \mod 3 = 0$ 或 $a_i \mod 3 = 0$时，$a_i \times i$ 是 $3$ 的倍数

记 $k = \lfloor \frac{x}{3}\rfloor$ ，$ m = 2*k - \frac{x}{2}$

若 $k * 2 < \frac{x}{2}$, 则一定不可能有一半的满足。

当$k * 2 \ge \frac{x}{2}$ , 则一定有 $m$个 $i$ 满足 $i \mod 3 = 0$ 且 $a_i \mod 3 = 0$，此时有 $A_{k}^{m} * C_{k}^{m}$ 中方法（有 $A_{k}^{m}$中排列 $m$ 个 $i$ 的方式，再有 $C_{k}^{m}$ 种 选择 $m$ 个 $i$ 的方式。

剩下的 $k-m$ 个满足 $i \mod 3 = 0$ 的 $i$ ，需放在  $i \mod 3 != 0$ 的 地方，有 $A_{n-k}^{k-m}$ 种排列方式。

其余的 $i$ 随便排列，有 $A_{n-k}^{n-k}$ 种方法。



答案为 $A_{k}^{m} * C_{k}^{m} *A_{n-k}^{k-m} * A_{n-k}^{n-k}$

```cpp
#include <bits/stdc++.h>
using namespace std;
  
typedef long long ll;
typedef pair<long long,long long> PLL;
typedef tuple<ll,ll,ll> TLLL;
const ll inf =  0x3f3f3f3f;
const ll INF = INT_MAX;
  
inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
   
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
   
void print(ll x){pt(x), puts("");}


const ll mod = 1e9+7;
ll fac[1000009];
ll ifac[1000009];
ll ksm(ll a,ll b){
    ll ans = 1;
    while(b){
        if(b&1)ans = ans * a % mod;
        a = a * a % mod;
        b >>= 1;
    }
    return ans;
}
ll C(ll a,ll b){
    return fac[a] * ifac[b] % mod * ifac[a-b] % mod;
}

ll A(ll n, ll m){
    return fac[n] * ifac[n-m] % mod;
}

void solve(){
    ll n = read();
    ll k = n/3;
    if (k * 2 < n/2 ){
        print(0);
    }
    else{
        ll m = k * 2 - n/2;
        ll use = k - m;
        ll t1 = (A(k, m) *  C(k, m) % mod );
        ll ans = (t1 * A(n - k, use) %mod )* A(n-k, n-k)%mod;
        print(ans);
    }
    
}

int main(){
    fac[0] = ifac[0] = 1;
    for(int i = 1; i <= 1000002; i++){
        fac[i] = fac[i-1] * i % mod;
    }
    ifac[1000002] = ksm(fac[1000002], mod-2);
    for(int i = 1000002-1; i >= 1; i--){
        ifac[i] = ifac[i+1] * (i+1) % mod;
    }
    ll t = 1;
    //t = read();
    while(t--){
        solve();
    }
}
```

# F.小红的小球染色期望

令 $dp_i$ 为 $n=i$ 时的期望。

易得$dp_0 = dp_1 = 0$, $dp_2 = 1$

考虑其他情况时，我们考虑选择的左端点，有$n-1$ 中选择，每种选择的概率为 $\frac{1}{n-1}$ 。

每种选择后，会剩下左右两段，每段结束的期望在 $n$ 较小的计算中可以得出。

观察发现左端的长度会从 $0$ 取到 $n-2$, 右端从 $n-2$ 取到 $0$，期望总和为$ \frac{1}{n-1} * 2 * \sum_{j=1}^{n-2} dp_j$（这可以用前缀和优化）。

加上这一次操作有 $dp_i =  \frac{1}{n-1} * 2 * \sum_{j=1}^{i-2} dp_j + 1$。

```cpp
#include <bits/stdc++.h>
using namespace std;
  
typedef long long ll;
typedef pair<long long,long long> PLL;
typedef tuple<ll,ll,ll> TLLL;
const ll inf =  0x3f3f3f3f;
const ll INF = INT_MAX;
  
inline ll read(){
    ll s = 0, w = 1; char ch = getchar();
    while (ch < 48 || ch > 57) { if (ch == '-') w = -1; ch = getchar(); }
    while (ch >= 48 && ch <= 57) s = (s << 1) + (s << 3) + (ch ^ 48), ch = getchar();
    return s * w;
}
   
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
   
void print(ll x){pt(x), puts("");}


const ll mod = 1e9+7;

ll ksm(ll a,ll b){
    ll ans = 1;
    while(b){
        if(b&1)ans = ans * a % mod;
        a = a * a % mod;
        b >>= 1;
    }
    return ans;
}

ll dp[1000009];
ll pre[1000009];
int main(){
    ll n = read();
    dp[2] = 1;
    pre[2] = 1;
    for(ll i=3;i<=n;i++){
        ll p = ksm(i-1, mod-2);
        dp[i] = (dp[i] + pre[i-2]*2%mod*p%mod)%mod;
        dp[i] = (dp[i] + 1)%mod;
        pre[i] = (pre[i-1] + dp[i])%mod;
    }
    print(dp[n]);
    
}
```