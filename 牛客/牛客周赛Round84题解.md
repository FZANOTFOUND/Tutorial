## A.小红的陡峭值（一）

由题意只有三个数完全相等时才会使陡峭值为0.

```python
a, b, c = map(int, input().split())
if a == b == c:
    print('Yes')
else:
    print("No")
```



## B.小红的陡峭值（二）

要让陡峭值尽可能小，我们肯定要让相邻的数尽可能相近。

不难想到可以把 $a$ 排序，这样总和一定最小。

升序排序和降序排序是等价的，有 $2$ 种。但如果所有数都一样，只能算 $1$ 种。

```python
n = int(input())
a = list(map(int, input().split()))
a.sort()
print(1 if len(set(a)) == 1 else 2, sum([abs(a[i+1]-a[i]) for i in range(n-1)]))
```



## C/D.小红的陡峭值（三）

不难想到计算每个位置被取了多少次（即贡献）。

可以用差分模拟每次选的过程，再求贡献数组。

```python
n, k = map(int, input().split())
a = list(map(lambda x : ord(x)-ord('a'), list(input())))
b = [abs(a[i+1]-a[i]) for i in range(n-1)]
diff = [0 for i in range(n)]
use = [0 for i in range(n-1)]
for l in range(0, n-k+1):
    diff[l] +=1
    diff[l+k-1] -= 1
pre = 0
for i  in range(n-1):
    use[i] = pre + diff[i]
    pre = use[i]
ans = 0
for i in range(n-1):
    ans += use[i] * b[i]
print(ans)
```



## E.小红的陡峭值（四）

不妨以 $1$ 为根节点。

我们可以枚举每颗子树，求子树和其余部分的陡峭值的差。

先用 $dfs$ 求出每个节点及其子树的陡峭值之和。

再枚举除了根节点的所有节点，求最小值。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll INF = 1e18+9;

//io functions
inline ll read(){ll x=0;short f=1;char c=getchar();while((c<'0'||c>'9')&&c!='-') c=getchar();if(c=='-') f=-1,c=getchar();while(c>='0'&&c<='9') x=x*10+c-'0',c=getchar();x*=f;return x;}  
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
inline void print(ll x){pt(x), puts("");}

void solve(){
    ll n = read();
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<=n-1;i++){
        ll u = read(),  v = read();
        g[u].push_back(v);
        g[v].push_back(u);
    }
    vector<ll> dp(n+1);
    vector<ll> fa(n+1);
    function<void(ll, ll)> dfs = [&](ll u, ll p){
        fa[u] = p;
        for(auto v:g[u]){
            if (v == p)continue;
            dfs(v, u);
            dp[u] += abs(u-v) + dp[v];
        }
    };
    dfs(1, 0);
    ll ans = INF;
    for(ll i=2;i<=n;i++){
        ll t1 = dp[1] - dp[i] - abs(i-fa[i]);
        ll t2 = dp[i];
        ans = min(ans, abs(t1 - t2));
    }
    print(ans);
}

int main(){
    ll t = 1;
    //t = read();
    while(t--){
        solve();
    }
}
```



## F/G.小红的陡峭值（五）

考虑贡献。

对确定的一组数 $(a, b)$ ,我们需要知道在 $n!$ 个排列中出现了多少次。( $(b, a)$ 不算)

其余的 $n-2$ 个数有 $(n-2)!$ 种排列方式，$(a, b)$ 插入其中有 $n-1$种方式。所以共出现  $(n-1)!$ 次。

考虑如何快速求出所有的 $\left | a-b \right |$ 的和。

我们先对 $a$ 排序，则比 $a_i$ 小的数在左侧，大的数在右侧。

用数组前后缀和即可快速算出$s_i = \sum_{j=1,j \ne i}^{n} \left | a_j - a_i \right |$ 。( $s_i = a_i * (i-1) - pre_{i-1} + surf_{i+1} - a_i * (n-i)$ )

假设 $t = \sum_{i=1}^{n} s_i$，则最后的答案为 $\frac{t * (n-1)!}{n!} = \frac{t}{n}$

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll MOD = 1e9+7;
//io functions
inline ll read(){ll x=0;short f=1;char c=getchar();while((c<'0'||c>'9')&&c!='-') c=getchar();if(c=='-') f=-1,c=getchar();while(c>='0'&&c<='9') x=x*10+c-'0',c=getchar();x*=f;return x;}  
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
inline void print(ll x){pt(x), puts("");}

//fast pow
ll ksm(ll a, ll b){ll res = 1;while(b){if(b&1){res=(res*a)%MOD;}a=(a*a)%MOD;b>>=1;}return res;}

void solve(){
    ll n = read();
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++){
        a[i] = read();    
    }
    sort(a.begin()+1, a.end());
    vector<ll> pre(n+2), surf(n+2);
    for(ll i=1;i<=n;i++) pre[i] = pre[i-1] + a[i];
    for(ll i=n;i>=1;i--) surf[i] = surf[i+1] + a[i];
    ll ans = 0;
    for(ll i=1;i<=n;i++){
        ans = (ans + (surf[i+1] - a[i] * (n-i) + a[i] * (i-1)- pre[i-1]+MOD))%MOD;
    }
    print(ans%MOD*ksm(n, MOD-2)%MOD);
}

int main(){
    ll t = 1;
    //t = read();
    while(t--){
        solve();
    }
}
```



