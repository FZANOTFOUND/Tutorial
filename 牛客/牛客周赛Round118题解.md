# A.小红的博弈

显然如果有至少 $3$ 个石子，则小紫可以行动，且行动时可以拿完所有的石子，小紫赢。

否则小红赢。

```py
n = int(input())
if n >= 3:
    print("purple")
else:
    print("red")
```

# B.小红选点

$O(n^2)$ 枚举每一对点即可。

```py
n = int(input())
p = [list(map(int, input().split())) for i in range(n)]
mx = -10**9
ans = []
for i in range(n):
    for j in range(i+1, n):
        dis = (p[i][0] - p[j][0]) ** 2 + (p[i][1] - p[j][1]) ** 2
        if dis > mx:
            mx = dis
            ans = p[i] +p[j]
print(*ans)
```



# C. 小红的矩形

显然如果 $x/y$ 坐标相同，则在 $x/y$ 方向上扩展；否则交换 $y$ 坐标即可。

```py
x1, y1, x2, y2 = map(int, input().split())
if x1 == x2:
    print(x1+1, y2, x2+1, y1)
elif y1 == y2:
    print(x1, y1+1, x2, y2+1)
else:
    print(x1, y2, x2, y1)
```



# D.小红拿石子1.0

显然从大到小取一遍一定最优。

```py
n = int(input())
a = sorted(map(int, input().split()), reverse=True)
ans = 0
for i in range(n):
    ans += max(0, a[i]-i)
print(ans)
```



# E.小红玩树

~~嫌这段烦的去看解法2~~

## 解法1

不妨以小红为根节点讨论。

若小红所在节点度为 $1$ ，则小红一定赢。

否则分两种情况讨论：

- 小红往小紫所在子树走，则枚举 $b$ -> $a$ 每一个节点作为中继节点，判断小红和小紫是否会相遇，并且小紫是否会在小红到达根节点前追上小紫。
- 小红不往小紫所在子树走，则判断小紫是否会在小红到达根节点前追上小紫。

```cpp
void solve(){
    ll n = read(), a = read(), b = read();
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<=n-1;i++){
        ll u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
    }
    vector<ll> dep(n+1), fa(n+1), w(n+1);
    function<void(ll, ll)> dfs = [&](ll u, ll p){
        fa[u] = p;
        dep[u] = dep[p]+1;
        if(g[u].size()==1){
            w[u] = 0;
            return;
        }
        ll mi = INF;
        for(auto v:g[u]){
            if(v == p) continue;
            dfs(v, u);
            mi = min(mi, w[v]);
        }
        w[u] = mi + 1;
    };
    dfs(a, 0);
    if(g[a].size()==0){// a 为根节点
        puts("red");
        return;
    }
    // 小红往小紫所在子树走
    vector<ll> vis(n+1);
    ll u = b;
    while(u!=a){
        // 枚举每个 a -> b 上的 u 为相遇节点
        ll dis1 = dep[u] - dep[a];
        ll dis2 = (dep[b]-dep[u]+1)/2;
        ll tot1 = dis1 + w[u];
        ll tot2 = (dep[b]-dep[u]+w[u]+1)/2;
		// 注意如果 w[u] 是往小紫走的最近根节点，则 dis1 < dis2 不会满足
        if(dis1<dis2&&tot1<=tot2){
            puts("red");
            return;
        }
        
        vis[u] = 1;
        u = fa[u];
    }
    
    // 小红不往小紫所在子树走
    ll rdis = INF;
    for(auto v:g[a]){
        // vis[v] 代表是否是向小紫所在子树走
        if(!vis[v]) rdis = min(rdis, w[v]+1);
    }
    ll pdis = dep[b] - 1;
    if(pdis >= rdis){
        puts("red");
    }
    else{
        puts("purple");
    }
}
```

## 解法2

事实上以 $b$ 为根节点，枚举 $a$ - > $b$ 中每一个节点作为中间节点更好写。

此时相当于只有一种情况。（包含了解法 $1$ 的两种情况）

```cpp
void solve(){
    ll n = read(), a = read(), b = read();
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<=n-1;i++){
        ll u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
    }
    vector<ll> dep(n+1), fa(n+1), w(n+1);
    function<void(ll, ll)> dfs = [&](ll u, ll p){
        fa[u] = p;
        dep[u] = dep[p]+1;
        if(g[u].size()==1&&u!=b){
            w[u] = 0;
            return;
        }
        ll mi = INF;
        for(auto v:g[u]){
            if(v == p) continue;
            dfs(v, u);
            mi = min(mi, w[v]);
        }
        w[u] = mi + 1;
    };
    dfs(b, 0);
    if(g[a].size()==0){
        puts("red");
        return;
    }
    ll u = a;
    while(u!=b){
        ll dis1 = dep[a] - dep[u];
        ll dis2 = (dep[u] - dep[b]+1)/2;
        ll tot1 = dis1 + w[u];
        if(dis1<dis2&&tot1<=dep[u]-dep[b]){
            puts("red");
            return;
        }
        u = fa[u];
    }
    puts("purple");
}
```



# F.小红拿石子2.0

注意到小紫的操作轮数为数组中的最大值。

题目即转化为小红能否在 $max_{a}$ 轮内删除掉所有数。

令 $cnt$ 为数组中 $max_{a}$ 出现的次数。

如果 $ cnt \le max_a$，则小红可以删除最大值直到只剩一个，再不停删除次大值直到剩一个数，再删除最后一个数（即原来的最大值），删除所有数，使得小紫无法执行下一步。

例如 $\texttt{1 1 3 3}$ ，小红删除 $3$，小紫操作，变为 $\texttt{2}$，小红操作删除所有数。

例如 $\texttt{1 1 2 3}$ ，小红删除 $2$，小紫操作，变为 $\texttt{2}$，小红操作删除所有数。

否则小紫会删除所有数，使得小红无法执行下一步。

```py
for _ in range(int(input())):
    n = int(input())
    a = list(map(int, input().split()))
    a.sort()
    if a.count(a[-1]) > a[-1]:
        print("purple")
    else:
        print("red")
            
```





# C++ 火车头

```cpp
// FZANOTFOUND
#include <bits/stdc++.h>
using namespace std;

#define pb push_back 
#define eb emplace_back 
#define fi first
#define se second
#define ne " -> "
#define sep "======"
#define fastio ios::sync_with_stdio(false);cin.tie(0);
#define all(a) a.begin(), a.end()

typedef long long ll;
typedef unsigned long long ull;
typedef long double db;
typedef pair<long long,long long> PLL;
typedef tuple<ll,ll,ll> TLLL;
const ll INF = (ll)2e18+9;
//const ll MOD = 1000000007;
const ll MOD = 998244353;
const db PI = 3.14159265358979323;

//io functions
inline void rd(ll &x){x=0;short f=1;char c=getchar();while((c<'0'||c>'9')&&c!='-') c=getchar();if(c=='-') f=-1,c=getchar();while(c>='0'&&c<='9') x=x*10+c-'0',c=getchar();x*=f;}  
inline ll read(){ll x=0;short f=1;char c=getchar();while((c<'0'||c>'9')&&c!='-') c=getchar();if(c=='-') f=-1,c=getchar();while(c>='0'&&c<='9') x=x*10+c-'0',c=getchar();x*=f;return x;}  
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
inline void print(ll x){pt(x), puts("");}
inline void print(PLL x){pt(x.fi), putchar(' '), pt(x.se), putchar('\n');}
inline void print(vector<ll> &vec){for(const auto t:vec)pt(t),putchar(' ');puts("");}
inline void print(const map<ll, ll>& g) {for(const auto& [key, value]:g){cout<<"key: "<<key<<ne<<value<<" ";}puts("");}
inline void print(vector<PLL> &vec){puts(sep);for(const auto v:vec){print(v);}puts(sep);}
inline void print(const map<ll, vector<ll>>& g) {for (const auto& [key, value] : g) { cout << "key: " << key << ne;for (const auto& v : value) {cout << v << " ";}cout << endl;}}

//fast pow
ll ksm(ll a, ll b=MOD-2, ll M=MOD){a%=M;ll res=1;while(b){if(b&1){res=(res*a)%M;}a=(a*a)%M;b>>=1;}return res;}

mt19937_64 rng(chrono::steady_clock::now().time_since_epoch().count());//rng()
ull randint(ull l, ull r){uniform_int_distribution<unsigned long long> dist(l, r);return dist(rng);}

void init(){
    
}

void solve(){
    
}

int main(){
    init();
    ll t = 1;
    //t = read();
    while(t--){
        solve();
    }
}
```