# A.Add Three

显然答案即为 $3 \times \frac{n}{3}$。

时间复杂度 $O(1)$。

```cpp
void solve(){
    print(read()/3*3);
}
```



# B.Maximize The Count

经典的 trick。

对于 $p_{i+1} - p_i = a_{p_{i+1}} - a_{p_i}$ 可变形为   $a_{p_i} - p_i = a_{p_{i+1}} - p_{i+1}$。

则将 $a_i$ 变为 $a_i - i$ 后，相同的元素可以组成一个子序列，统计一下那个数字出现最多即可。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    unordered_map<ll, ll> cnt;
    for(ll i=1;i<=n;i++){
        cnt[read()-i]++;
    }
    ll mx = 0;
    for(auto [k, v]:cnt){
        mx = max(mx, v);
    }
    print(mx);
}
```



# C.Permutation Swapping

手玩一下可以发现，当 $n \ge 4$ 时，可以任意置换这个序列，则一定可以有序。

当 $n = 3$ 时，只有 $\texttt{1 2 3}$ 和 $\texttt{3 2 1}$ 可以。

当 $n <= 2$ 时，只有 $\texttt{1...n}$ 可以。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    if(n >= 4){
        puts("YES");
    }
    else if(n == 3){
        if(a == vector<ll> {0, 1, 2, 3}|| a == vector<ll> {0, 3, 2, 1}){
            puts("YES");
        }
        else{
            puts("NO");
        }
    }
    else{
        ll f = 1;
        for(ll i=1;i<=n;i++) f&=(a[i]==i);
        puts(f?"YES":"NO");
    }
}
```



# D.Two Options

显然若要将所有元素变成一样，我们首先要使得 $\sum \limits_{i=1}^{n} a_i$ 是  $n$ 的倍数。

因此除了余数为$0$ 的情况，我们需要进行操作一 $n-\sum \limits_{i=1}^{n} a_i \% n$ 次。

设最终的目标为 $t$。

对于 $a_i < t$ 的元素，可以用操作一或者操作二提升。

对于 $a_i > t$ 的元素，只能用操作二。

因此增加的操作数量一定大于等于减少的数量，即最终操作数量即为增加的操作数量。

即 $\sum \limits_{a_i < t} (t-a[i])$。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1);
    ll sum = 0;
    for(ll i=1;i<=n;i++) a[i] = read(), sum += a[i];
    ll t = (sum%n+n)%n;
    ll need = t==0?0:(n-t);
    ll tar = (sum + need)/n;
    ll ans = 0;
    for(ll i=1;i<=n;i++){
        if(a[i] < tar){
            ans += (tar-a[i]);
        }
    }
    print(ans);
}
```



# E.Not Equal

手玩一下可以发现，元素的变化不会太大。

极端情况下，例如 $\texttt{2 2 3}$ ，我们可能 第 $2$ 个 $2$ 变到 $4$ 比变到 $1$ 更优。

我们可以猜测，$a_i$ 最终的值属于 $[a_i−2,a_i+2]$ 。

则 $dp$ 计算即可。

时间复杂度 $O(25n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    vector<array<ll, 5>> cost(n+1, {0, 0, 0, 0, 0});
    for(ll i=1;i<=n;i++) cost[i][3] = read(), cost[i][4] = 2*cost[i][3];
    for(ll i=1;i<=n;i++) cost[i][1] = read(), cost[i][0] = 2*cost[i][1];
    vector<array<ll, 5>> dp(n+1, {INF, INF, INF, INF, INF});
    for(ll d=0;d<=4;d++){
        if(a[1]+d-2<1) continue;
        dp[1][d] = cost[1][d];
    }
    for(ll i=2;i<=n;i++){
        for(ll d1=0;d1<=4;d1++){
            if(a[i]+d1-2<1) continue;
            for(ll d2=0;d2<=4;d2++){
                if(a[i-1]+d2-2<1) continue;
                if(a[i]+d1==a[i-1]+d2) continue;
                dp[i][d1] = min(dp[i][d1], dp[i-1][d2]+cost[i][d1]);
            }
        }
    }
    print(min({dp[n][0], dp[n][1], dp[n][2], dp[n][3], dp[n][4]}));
}
```



# F.Alone

不难想到对每个格子计算贡献。



- 对于原来所在行列都没有黑格的格子，设总共有 $cnt_x$ 个不同的 $x_i$，  $cnt_y$ 个不同的 $y_i$，则其数量为 $(n-cnt_x+1)\times (m-cnt_y+1)$ 个。

  除了其所在行列外，所有初始不是黑色的格子都可以随便取，这部分格子有 $n*m-k-n-m+1$ 个。

  则这类格子的总贡献为 $(n-cnt_x+1)\times (m-cnt_y+1) * 2^{n*m-k-n-m+1}$。

- 对于原来所在行列都只有当前格子是黑色的格子，设其数量为 $cnt$ 个。

  除了其所在行列外，所有初始不是黑色的格子都可以随便取，这部分格子有 $n*m-k-n-m+2$ 个。

  则这类格子的总贡献为 $cnt * 2^{n*m-k-n-m+2}$。

  时间复杂度 $O(k)$。

  **注意快速幂判断指数是不是大于等于 $0$。**

```cpp
void solve(){	
	ll n = read(), m = read(), k = read();
    unordered_map<ll, ll> r, c;
    vector<PLL> p(k);
    for(ll i=0;i<k;i++){
        p[i] = {read(), read()};
        r[p[i].fi]++;
        c[p[i].se]++;
    }
    ll cntr = 0, cntc = 0;
    for(auto [k, v]:r) cntr++;
    for(auto [k, v]:c) cntc++;
    ll ans = 0;
    if(n*m-k-n-m+1>=0) ans = (n-cntr)*(m-cntc)%MOD*ksm(2, n*m-k-n-m+1)%MOD;
    ll cnt = 0;
    for(auto [x, y]:p){
        if(r[x]>1||c[y]>1) continue;
        cnt++;
    }
    if(n*m-k-n-m+2>=0) ans = (ans + cnt*ksm(2, n*m-k-n-m+2)%MOD)%MOD;
    print(ans);
}
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
    //fastio;cin>>t;
    t = read();
    while(t--){
        solve();
    }
}
```

