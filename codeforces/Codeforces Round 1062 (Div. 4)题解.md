[Codeforces Round 1062 (Div. 4)](https://codeforces.com/contest/2167)

# A.Square?

~~你wa了可以不打acm了~~

判断四个数是不是都相等即可。

时间复杂度 $O(1)$。

```cpp
void solve(){
    ll a = read(), b = read(), c = read(), d = read();
    if(a == b && b == c&& c == d){
        puts("YES");
    }
    else{
        puts("NO");
    }
}
```





# B.Your Name

排序后判断两个字符串是否相等即可。

时间复杂度 $O(nlogn)$。

```cpp
void solve(){
    ll n;cin>>n;
    string s1, s2;
    cin>>s1>>s2;
    sort(all(s1));
    sort(all(s2));
    puts(s1==s2?"YES":"NO");
}
```



# C.Isamatdin and His Magic Wand!

显然如果又有奇数又有偶数一定能排序，否则不能。

时间复杂度 $O(nlogn)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n);
    ll cnt0 = 0, cnt1 = 0;
    for(ll i=0;i<n;i++){
        a[i] = read();
        cnt0 += (a[i]%2==0);
        cnt1 += (a[i]%2==1);
    }
    if(cnt0&&cnt1)sort(all(a));
    print(a);
}
```



# D. Yet Another Array Problem

由于 $2 \times 3 \times 5 \times 7 \times 11 \times 13 \times 17 \times 19 \times 23 \times 29 \times 31 \times 37 \times 41 \times 43 \times 47 \times 53 = 32589158477190044730 > 10^{18}$， 因此遍历 $2$  ~ $60$ 一定能找到一个满足题意的答案。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n);
    for(ll i=0;i<n;i++) a[i] = read();
    ll ans = INF;
    for(auto v:a){
        for(ll i=2;i<=60;i++){
            if(__gcd(v, i)==1){
                ans = min(ans, i);
            }
        }
    }
    print(ans);
}
```



# E.khba Loves to Sleep!

二分判定最长时间，根据最优解构造答案即可。

二分最长时间时，对于每个位置 $v$，我们知道此时 $[max(0, v-mid), min(x, v+mid)]$ 区间内不能有点。统计所有的区间并合并。计算此时最多能放多少个点。判断能不能放下 $k$ 个点。

构造答案时在区间间的空位内放即可。若没有选出 $k$ 个点，此时所有的坐标一定被全覆盖，任意选取没选过的即可，

时间复杂度 $O(nlogx)$。

```cpp
void solve(){
    ll n = read(), k = read(), x = read();
    vector<ll> a(n);
    for(ll i=0;i<n;i++) a[i] = read();
    sort(all(a));
    function<ll(ll)> check = [&](ll mid){
        vector<PLL> inv;
        for(auto v:a){
            inv.pb({max(0ll, v-mid), min(x, v+mid)});
        }
        sort(all(inv));
        vector<PLL> merge;
        for(auto [l, r]:inv){
            if(merge.empty()||l>merge.back().se+1) merge.pb({l, r});
            else merge.back().se = max(merge.back().se, r);
        }
        ll tot = x + 1;
        for(auto [l, r]:merge){
            tot -= (r-l+1);
        }
        return tot >= k;
    };
    ll l = 0, r = x, best = 0;
    while(l <= r){
        ll mid = (l + r)>>1;
        ll merge = check(mid);
        if(merge){
            best = mid;
            l = mid + 1;
        }
        else{
            r = mid - 1;
        }
    }
    vector<PLL> inv;
    for(auto v:a){
        inv.pb({max(0ll, v-best), min(x, v+best)});
    }
    sort(all(inv));
    vector<PLL> merge;
    for(auto [l, r]:inv){
        if(merge.empty()||l>merge.back().se+1) merge.pb({l, r});
        else merge.back().se = max(merge.back().se, r);
    }
    vector<ll> ans;
    ll left = k;
    for(ll i=0;(i<merge[0].fi)&&left;i++,left--){
        ans.pb(i);
    }
    for(ll idx=1;idx<merge.size()&&left;idx++){
        for(ll i=merge[idx-1].se+1;(i<merge[idx].fi)&&left;i++,left--){
            ans.pb(i);
        }
    }
    for(ll i=merge.back().se+1;i<=x&&left;i++,left--){
        ans.pb(i);
    }
    map<ll, ll> use;
    for(auto v:ans) use[v] = 1;
    ll idx = 0;
    while(ans.size()<k){
        while(use[idx]){
            idx++;
        }
        ans.pb(idx);
        use[idx] = 1;
        idx++;
    }
    print(ans);
}
```



# F. Tree, TREE!!!

以根为 $r$ 时，若 $u$ 的子树大小 $>=k$ 则 $u$ 在答案的集合内。记此时一种方案为 $(r, u)$。

不考虑限制条件，则有 $n^2$ 种方案。

不妨以 $1$ 为根节点统计每个节点的子树的大小。

对于节点 $u$，可分为 $u$ 的子树和其余两个树。

若 $u$ 的子树的大小 $<k$ ，则对于所有在其余树中的点，以其为根的时候，$(r, u)$ 一定不是一个合法的方案。

反之同理。

因此遍历所有点减去不合法的方案即可。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read(), k = read();
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<=n-1;i++){
        ll u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
    }
    vector<ll> fa(n+1), sz(n+1);
    function<void(ll, ll)> dfs = [&](ll u, ll p){
        sz[u] = 1;
        fa[u] = p;
        for(auto v:g[u]){
            if(v == p) continue;
            dfs(v, u);
            sz[u] += sz[v];
        }
    };
    dfs(1, 0);
    ll ans = n * n;
    for(ll u=2;u<=n;u++){
        if(sz[u]<k) ans -= (n-sz[u]);
        if(n-sz[u]<k) ans -= sz[u]; 
    }
    print(ans);
}
```



# G. Mukhammadali and the Smooth Array

显然对于更改的数，总有一种方案能够使得最终合法。因此考虑保留下来的数字的最大价值。

令 $dp_i$ 为 以 $i$ 为节点时，保留下来的数字的最大价值。初始 $dp_i = c_i$。

对于 $j\in[1, n-1]$ ，若 $a_j <= a[i]$ ，则此时 $j$ 也可以保留，更新 $dp_i$ 为 $max(dp_i, dp_j + c[i])$。

答案即为 $\sum \limits_{i=1}^{n} c_i - \max \limits_{i=1}^{n} dp_i$。

时间复杂度 $O(n^2)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1), c(n+1), dp(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    for(ll i=1;i<=n;i++) c[i] = read();
    for(ll i=1;i<=n;i++){
        dp[i] = c[i];
        for(ll j=1;j<i;j++){
            if(a[j]<=a[i]){
                dp[i] = max(dp[i], dp[j] + c[i]);
            }
        }
    }
    print(accumulate(all(c), 0ll)-*max_element(all(dp)));
}
```

离散化 + 树状数组/线段树 可以 $O(nlogn)$

```cpp
class BIT{
    public:
    ll n_;
    vector<ll> c;
    BIT(ll n){
        n_= n;
        c.resize(n+1);
    }
    void update(ll x, ll d){
        for(;x<=n_;x+=(x&(-x))) c[x] = max(c[x], d);
    }
    ll query(ll x){
        ll res = 0;
        for(;x;x-=(x&(-x))){
            res = max(res, c[x]);
        }
        return res;
    }
};

void solve(){
    ll n = read();
    vector<ll> a(n+1), c(n+1), dp(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    vector<ll> b = a;
    sort(all(b));
    map<ll, ll> name;
    for(ll i=1,idx=1;i<=n;i++){
        if(!name[b[i]]){
            name[b[i]] = idx;
            idx++;
        }
    }
    BIT bit(2*n);
    for(ll i=1;i<=n;i++) a[i] = name[a[i]];
    for(ll i=1;i<=n;i++) c[i] = read();
    for(ll i=1;i<=n;i++){
        dp[i] = c[i] + bit.query(a[i]);
        bit.update(a[i], dp[i]);
    }
    print(accumulate(all(c), 0ll)-*max_element(all(dp)));
}
```





# 火车头

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
const ll MOD = 1000000007;
//const ll MOD = 998244353;
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