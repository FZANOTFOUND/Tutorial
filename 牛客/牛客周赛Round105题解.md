
<img src="https://uploadfiles.nowcoder.com/images/20250817/226800108_1755435797818/B6C8F80B37D5731009B15EA211B72CE3" alt="描述" width="400" height="270">

~~疑似首刀A~~
# A. 小苯的xor构造

易得 $k \bigoplus 0 = k$，输出 `k 0` 即可。


```python
print(input(), 0)
```



# B.小苯的权值计算

按题意计算即可

```python
from math import gcd
n = int(input())
a = [0] + list(map(int, input().split()))
b = [0]
g = 0
for i in range(1, n):
    g = gcd(g, a[i]^a[i+1])
print(g)
```



# C.小苯的01矩阵构造

考虑初始全 $0$ 的情况下进行翻转操作。

不难发现，每次翻转，行和列的异或和均会变化，因此$\rm{sum}_r + \rm{sum}_c$ 一定为偶数。

当 $k$ 为奇数时无解，$k$ 为偶数时在对角线放置 $\frac{k}{2}$ 个 $1$ 即可。

```python
n, k = map(int, input().split())
if k % 2 == 1:
    print(-1)
else:
    g = [[0 for i in range(n)] for j in range(n)]
    for i in range(k//2):
        g[i][i] = 1
    for i in g:
        print(*i, sep='')
```



# D.小苯的重排构造

不难发现 $gcd$ 的值只有 $1, 2$ 两种，其中 $2$ 只能由 $2, 2$ 产生。

我们可以把 $gcd(a_i, a_{i+1}) = 2$ 视作 $gcd(a_i, a_{i+1}) = 1$ 基础上 $+1$，只需考虑如何 $ +1$。

令 $a$ 中由 $c_1$ 个 $1$ , $c_2$ 个 $2$ 。

不难得出  可行的 $k$ 的范围为 $[max(c2 - c1 - 1, 0) + n - 1, c2 - 1 + n - 1]$，对应 $121212$  和 $222111$ 两种情况。

满足条件的情况下，我们可以先在开头放置 $k - (n-1) + 1$ 个 $2$，在交替放置 $1$, $2$，即可构造出 $k$。

特判 全 $1$ 时 ，$k$ 只能为 $n-1$。

```python
n, k = map(int, input().split())
a = [0] + list(map(int, input().split()))
c1 = c2 = 0
for i in range(1, n+1):
    c1 += a[i] == 1
    c2 += a[i] == 2
if c1 == n:
    if k == n-1:
        print(*a[1:])
    else:
        print(-1)
else:
    if max(0, c2 - c1 - 1) + n - 1 <= k <= c2 - 1 + n - 1:
        ans = []
        for i in range(k-(n-1) + 1):
            ans.append(2)
        c2 -= k-(n-1) + 1
        for i in range(min(c1, c2)):
            ans.append(1)
            ans.append(2)
        ans += [1] * (c1 - c2)
        print(*ans)
    else:
        print(-1)
```



# E.小苯的xor图

看到异或和考虑拆位。

对每一位考虑，$w_i \in {0, 1}$。

观察到长度为 $2$ 的简单路径可以由点的邻居和点的邻居的邻居构成。

因此可以统计每个点周围有几个 $1$ ,几个 $0$。

计算时遍历 $u$ 的所有邻居，因为我们已经处理了每个点周围有几个 $1$ ,几个 $0$，因此此时可以直接计算出 $u - v $为起始的所有路径的异或和。

每条路径均会计算两次，因此最后要把答案除 $2$。

注意 $u$ 自己也是点的邻居的邻居，计算时要去掉自己。

时间复杂度$O(32 * 2 * m)$

```cpp
void solve(){
    ll n = read(), m = read();
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    vector<vector<ll>> w(32, vector<ll>(n+1));
    for(ll i=1;i<=n;i++){
        for(ll bit=31;bit>=0;bit--){
            if((a[i]>>bit)&1){
                w[bit][i] = 1;
            }
        }
    }
    vector<vector<ll>> g(n+1);
    vector<PLL> egs;
    vector<ll> cnei(n+1);
    for(ll i=1,u,v;i<=m;i++){
        u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
        egs.pb({u, v});
        cnei[u]++;
        cnei[v]++;
    }
    ll ans = 0;
    for(ll bit=31;bit>=0;bit--){
        vector<ll> nei(n+1);
        ll t = 0;
        for(ll i=1;i<=n;i++){
            for(auto v:g[i]){
                nei[i] += w[bit][v];
            }
        }
        for(ll i=1;i<=n;i++){
            if(w[bit][i]==1){
                for(auto v:g[i]){
                    if(w[bit][v]==1){
                        t += (nei[v]-1);
                    }
                    else{
                        t += cnei[v] - nei[v];
                    }
                }
            }
            else{
                for(auto v:g[i]){
                    if(w[bit][v]==0){
                        t += nei[v];
                    }
                    else{
                        t += (cnei[v] - nei[v] - 1);
                    }
                }
            }
        }
        ans = (ans + t * ((1<<bit)%MOD)%MOD)%MOD;
        //print(t);
    }
    print(ans*ksm(2, MOD-2)%MOD);
}  
```



# F. 小苯的前缀gcd构造

比较神秘的复杂度，加了三个剪枝就过了。

不难发现，如果 $b_i$ 不是 $b_{i+1}$ 的倍数，则 $f(i+1) = 1$，这和选择 $b_{i+1} = 1$ 是一样的效果。

因此我们可以搜索所有的 $b_i$ 是 $b_{i+1}$ 的倍数的序列，暴力求出每一种的答案。

但是直接交会$T$，可以加上以下几个剪枝：

- $x < n$ 时一定无解
- $x \% n = 0$ 时输出 $n$ 个 $\frac{x}{n}$
- 第一个数的范围只可能在 $[\lceil \frac{x}{n} \rceil, min(x, m)]$ 中。

```python
g = [[] for i in range(51)]
g[1].append(1)
for i in range(2, 51):
    for j in range(1, i+1):
        if i % j == 0:
            g[i].append(j)
            
def find(n, m, x):
    for fi in range(min(m, x),(x+n-1)//n-1,-1):
        stk = [[[fi], 1, fi]]
        while stk:
            v, s, xx = stk.pop()
            if s == n:
                if xx == x:
                    return v
                continue
            la = v[-1]
            for ne in g[la]:
                stk.append([v+[ne],s+1,xx+ne])
    return [-1] 
                    
for _ in range(int(input())):
    n, m, x = map(int, input().split())
    if x < n:
        print(-1)
    elif x % n == 0:
        print(*[x//n for i in range(n)])
    else:
        print(*find(n, m, x))
```



