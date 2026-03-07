# A.无穷无尽的力量

模拟即可。

```cpp
void solve(){
    ll n;cin>>n;
    for(ll i=0;i<n;i++)cout<<'a';
    cout<<'b';
    for(ll i=0;i<n;i++)cout<<'a';
}
```

# B.无穷无尽的字符串

不妨计算 $[1:x]$ 的答案 $ans_x$，则有 $ans_{x,a} = \lceil \frac{n}{3} \rceil $,$ans_{x,b} = \lceil \frac{n-1}{3} \rceil $,$ans_{x,c} = \lceil \frac{n-2}{3} \rceil $。

则答案为 $ans_{r} - ans{l-1}$。

```cpp
array<ll, 3> cal(ll x){
    return {(x+2)/3,(x+1)/3,x/3};
}
void solve(){
    ll l,r;cin>>l>>r;
    auto [x,xx,xxx] = cal(r);
    auto [y,yy,yyy] = cal(l-1);
    cout<<x-y<<' '<<xx-yy<<' '<<xxx-yyy<<'\n';
}
```

# C.无穷无尽的力量2.0

手玩可以发现大样例（至少 $3 \times 4$）下一定能走完所有的点。

当 $min(n, m) = 1$ 时，无法跳动，答案为 $1$。

当 $min(n, m) = 2$ 时，放在第一列第一行，则此时每个奇数列都可以选一个，答案为 $ \lceil \frac{max(n,m)}{2}  \rceil $。

当 $n = m = 3$ 时，放在第一列第一行，可以走到除了中心之外的所有位置，答案为 $8$。

```cpp
void solve(){
    ll n,m;cin>>n>>m;
    if(min(n, m)==1){
        cout<<1<<'\n';
    }
    else if(min(n, m)==2){
        cout<<(max(n, m)+1)/2;
    }
    else if(n==3&&m==3){
        cout<<8<<'\n';
    }
    else{
        cout<<n*m<<'\n';
    }
}
```

# D.无穷无尽的小数

由小学奥数，注意到相当于给了 $x = \frac{a}{\underbrace{9\ldots9}_{n}}$, $y = \frac{b}{\underbrace{9\ldots9}_{m}}$。

所以可以通分到 $n \times m$ 个 $9$ 后计算答案。（$c++ 要高精度$）。

注意如果通分后 $x$ 分母小于 $y$，则需要加上 $\underbrace{9\ldots9}_{n 
\times m}$，相当于借 $1$。

```py
n,m = map(int, input().split())
a = int(input() * m)
b = int(input() * n)
if a < b:
    a += int('9'*(n*m))
print(n*m)
print(str(a-b).zfill(n*m))
```

# E.无穷无尽的树

对于一个节点，我们需要知道除了叶子结点外深度最大的节点出现了几次，其答案可以由其儿子节点转移过来。

定义一个节点的权值为 ${mxdep, cnt}$（最大深度和出现次数）。

如果当前节点是叶子节点，我们可以认为其权值为 $\{-1, 0\}$。

否则，其初始权值为 $\{dep_u, 0\}$。

接下来，合并其所有子节点的权值 ${mxdep2, cnt2}$ 到当前节点。

如果 $mxdep2 > mxdep$ ，更新权值为 ${mxdep2, cnt2}$。

如果 $mxdep2 = mxdep$ ，更新权值为 ${mxdep, cnt + cnt2}$。

否则无变化。


$dfs$ 的时候统计答案即可。

```cpp
void solve(){
    ll n;cin>>n;
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<n;i++){
        ll u, v;cin>>u>>v;
        g[u].pb(v);
        g[v].pb(u);
    }
    vector<ll> dep(n+1), ans(n+1);
    function<void(ll, ll)> dfs1 = [&](ll u, ll p){
        dep[u] = dep[p]+1;
        for(auto v:g[u]){
            if(v == p) continue;
            dfs1(v,u);
        }
    };
    dfs1(1,0);
    function<PLL(PLL,PLL)> done = [&](PLL now, PLL res){
        if(res.fi==-INF) return now;
        if(res.fi > now.fi) now = res;
        else if(res.fi==now.fi) now.se += res.se;
        return now;
    };
    function<PLL(ll, ll)> dfs2 = [&](ll u, ll p){
        PLL now = {dep[u], 1};
        ll f = 0;
        for(auto v:g[u]){
            if(v == p) continue;
            f = 1;
            PLL res = dfs2(v,u);
            now = done(now, res);
        }
        if(!f){
            now = {-INF,0};
        }
        ans[u] = now.se;
        return now;
    };
    dfs2(1,0);
    for(ll i=1;i<=n;i++){
        cout<<ans[i]<<" \n"[i==n];
    }
}
```

# F.无穷无尽的数

不妨计算 $[1:p]$ 的答案 $ans_p$。

定义 $x$ 的长度为 $n$， $ans_n$ 为 $t$。

设能完整取 $k$ 段

对于能完整取的所有段，不考虑后续数字的情况下，其答案为 $ t * ((10^n)^{k-1} + .... + (10^n)^{0}) = t * \frac{(10^n)^k-1}{10^n-1}$。

余下的部分，我们可以在上一步的基础上遍历每一位，更新答案为 $(ans * 10 + x_i)\% mod$。

则区间 $[l,r]$的答案为 $ans_r - ans_l * 10 ^ {r-l+1}$（要左对齐 $[1:l]/[1:r]$ 对应的数字）。

```cpp
void solve(){
    ll n, l, r;cin>>n>>l>>r;
    string s;cin>>s;
    ll full=0, pw=1;
    for(auto v:s) full = (full*10 + v-48)%MOD,pw=pw*10%MOD;
    function<ll(ll)> cal = [&](ll x){
        ll t = x/s.size();
        ll res = ksm(pw-1+MOD,MOD-2)%MOD * ((ksm(pw, t)-1+MOD)%MOD)%MOD;
        res = res * full%MOD;
        for(ll i=0;i<x%s.size();i++){
            res = (res * 10 + s[i] - '0')%MOD;
        }
        return res;
    };
    ll resl = cal(l-1);
    ll resr = cal(r);
    resl = (resl * ksm(10, (r-l+1)))%MOD;
    cout<<((resr-resl+MOD)%MOD+MOD)%MOD;
}
```

c++火车头
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
    t = read();
    while(t--){
        solve();
    }
}
```
