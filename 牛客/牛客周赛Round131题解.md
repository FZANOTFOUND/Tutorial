# A.ICPC Balloons

按题意模拟即可

时间复杂度 $O(1)$。

```cpp
void solve(){
    cout<<vector<string>{"red","orange","blue","green"}[getchar()-'A'];
}
```



# B.String Covering

显然如果有一个 $1$ 周围没有 $1$ 则不可能。

时间复杂度 $O(n)$。

```cpp 
void solve(){
    ll n;cin>>n;
    string s;cin>>s;
    s = ' ' + s + ' ';
    for(ll i=1;i<=n;i++){
        if(s[i] == '1'){
            if(!(s[i-1]=='1'||s[i+1]=='1')){
                cout<<"NO\n";
                return;
            }
        }
    }
    cout"YES\n";
}
```



# C.Get The Sequence

对 $b$ 中的每一个元素，贪心找 $a$ 中第一个比其大的元素即可。

时间复杂度 $O(n+m)$。

```cpp
void solve(){
    ll n = read(), m = read();
    vector<ll> a(n+1), b(m+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    for(ll i=1;i<=m;i++) b[i] = read();
    ll idx1 = 1, idx2 = 1;
    while(idx2<=m){
        while(idx1<=n&&a[idx1]<b[idx2]){
            idx1++;
        }
        if(idx1>n||a[idx1]<b[idx2]){
            puts("NO");
            return;
        }
        idx1++;
        idx2++;
    }
    puts("YES");
}
```



# D.Longest Subsequence

令 $dp_i$ 为以 $a_i$ 结尾的最长长度， $ans_{i, j}$ 为前 $i$ 个元素中，序列末尾为 $j$ 的最长长度。

则有  $dp_i = max(ans_{i-1,a[i]-1}, ans_{i-1,a[i]+1})+1$。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    vector<ll> ans(n+2), dp(n+1);
    for(ll i=1;i<=n;i++){
        dp[i] = max(ans[a[i]-1], ans[a[i]+1]) + 1;
        ans[a[i]] = max(ans[a[i]], dp[i]);
    }
    print(*max_element(all(ans)));
}

```



# E.Eat The Candy

枚举每一个作为最终剩下的，把左边右边所有元素合并起来即可。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1), aa;
    for(ll i=1;i<=n;i++) a[i] = read();
    aa = a;
    ll mx = *max_element(all(a));
    vector<ll> pre(n+2), surf(n+2);
    for(ll i=2;i<=n;i++){
        ll t = min(aa[i], aa[i-1]);
        pre[i] = pre[i-1] + t;
        aa[i] -= t;
        aa[i-1] -= t;
    }
    aa = a;
    for(ll i=n-1;i>=1;i--){
        ll t = min(aa[i], aa[i+1]);
        surf[i] = surf[i+1] + t;
        aa[i] -= t;
        aa[i+1] -= t;
    }
    ll ans = 0;
    for(ll i=1;i<=n;i++){
        ans = max(ans, pre[i-1]+surf[i+1]+a[i]);
    }
    print(ans);
}
```



# F.Bracket Coloring

将 $($, $)$ 看做一组。则我们可以把所有右括号映射到左括号上。

建图，对于所有相邻相同的括号间连边，则一个连通分量里的元素一定是 $0101...$ 或者 $10101..$ $2$ 种。对于不同的连通分量，则没有限制。

因此若有 $c$ 个连通分量，则答案为 $2^c$。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n;cin>>n;
    string s;cin>>s;
    s = ' ' + s;
    vector<ll> left(n+1);
    vector<ll> stk;
    for(ll i=1;i<=n;i++){
        if(s[i]=='(') stk.pb(i);
        else left[i] = stk.back(),stk.pop_back();
    }
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<=n;i++){
        if(s[i]==s[i-1]){
            if(s[i]=='('){
                g[i].pb(i-1);
                g[i-1].pb(i);
            }
            else{
                g[left[i]].pb(left[i-1]);
                g[left[i-1]].pb(left[i]);
            }
        }
    }
    ll cnt = 0;
    vector<ll> vis(n+1);
    for(ll i=1;i<=n;i++){
        if(s[i]=='('&&!vis[i]){
            cnt++;
            queue<ll> q;
            q.push(i);
            while(!q.empty()){
                auto u = q.front();q.pop();
                vis[u] = 1;
                for(auto v:g[u]){
                    if(!vis[v]){
                        vis[v] = 1;
                        q.push(v);
                    }
                }
            }
        }
    }
    print(ksm(2, cnt));
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
    t = read();
    while(t--){
        solve();
    }
}


```

