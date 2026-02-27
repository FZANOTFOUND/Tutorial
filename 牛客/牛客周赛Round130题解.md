
# A.红美铃的访客登记

模拟即可

时间复杂度 $O(n)$。
```cpp
void solve(){
    string s;cin>>s;
    ll i=0;
    while(s[i]=='0') i++;
    cout<<s.substr(i, s.size())<<'\n';
}
```

# B.爱丽丝的魔力零件分类

先找到在一行/列上的三个点，判断另一个点是否在中间即可。

时间复杂度 $O(n^2)$。
```cpp
void solve(){
    ll n;cin>>n;
    vector<vector<char>> g(n, vector<char>(n));
    vector<PLL> p;
    map<ll, ll> cntx, cnty;
    for(ll i=0;i<n;i++){
        for(ll j=0;j<n;j++){
            cin>>g[i][j];
            if(g[i][j]=='*') {
                p.pb({i, j});
                cntx[i]++;
                cnty[i]++;
            }
        }    
    }
    ll f = 0, t = -1;
    for(auto [k, v]:cntx){
        if(v == 3){
            f = 1;
            t = k;
        }
    }
    if(!f){
        for(auto [k, v]:cnty){
            if(v == 3){
                t = k;
            }
        }
    }
//     cout<<f<<'\n';
    if(f){
        ll toty = 0;
        for(auto [xx, yy]:p){
            if(xx == t){
                toty += yy;
            }
        }
        toty/=3;
        for(auto [xx, yy]:p){
            if(xx != t){
                if(yy == toty){
                    puts("T");
                }
                else{
                    puts("L");
                }
                return;
            }
        }
    }
    else{
        ll totx = 0;
        for(auto [xx, yy]:p){
            if(yy == t){
                totx += xx;
            }
        }
        totx/=3;
        for(auto [xx, yy]:p){
            if(yy != t){
                if(xx == totx){
                    puts("T");
                }
                else{
                    puts("L");
                }
                return;
            }
        }
    }
    
}

```


# C.博丽大结界的稳定轴心

如果有度 $> 3$ 的点，则一定不可能是二叉树。

否则所有度 $ \le 2$ 的点都可以是根。

时间复杂度 $O(n)$。

```cpp
void solve(){
   ll n = read();
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<n;i++){
        ll u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
    }
    ll f = 1;
    for(ll i=1;i<=n;i++){
        if(g[i].size()>3) f= 0;
    }
    if(!f){
        print(0);
        return;
    }
    ll cnt = 0;
    for(ll i=1;i<=n;i++){
        if(g[i].size()<=2) cnt++;
    }
    print(cnt);
}
```

# D.魔法人偶的十进制校准

由小学奥数得$\frac{xy}{99}$ 的小数是 $0.xyxyxy$，循环节为 $xy$。

根据 $a$的奇偶凑一下即可。

时间复杂度 $O(1)$。

```cpp
void solve(){
    ll a, b;cin>>a>>b;
    a--;
    if(1 <= b && b <= 8){
        if(b % 3 == 0){
            if(a % 2 == 0)cout<<b<<1<<' '<<99<<'\n';
            else cout<<1<<b<<' '<<99<<'\n';
        }
        else{
            cout<<b<<' '<<9<<'\n';
        }
    }
    else if(b == 0){
        if(a % 2 == 0) cout<<"1 99\n";
        else cout<<"10 99\n";
    }
    else{
        if(a % 2 == 0) cout<<"91 99\n";
        else cout<<"19 99\n";
    }
}
```

# E.爱丽丝的人偶圆舞曲

对于一个特定的 $d$，可以用 $dp$ 求出最小改动。则只需要枚举每个 $d$ 找到最小即可。

令 $dp[i][p]$ 为第 $i$ 个字符为 $p$ 时，前 $i$ 个字符的最小修改次数。

则
$$
dp[i][p] =
\begin{cases}
\min\Big(
dp[i-1][(p-d+26)\bmod 26],\;
dp[i-1][(p+d+26)\bmod 26]
\Big),
& \text{若 } p = s_i
\\[1em]
\min\Big(
dp[i-1][(p-d+26)\bmod 26],\;
dp[i-1][(p+d+26)\bmod 26]
\Big) + 1,
& \text{若 } p \ne s_i
\end{cases}
$$


时间复杂度 $O(26*26*n)$。

```cpp
void solve(){
    string s;cin>>s;
    ll n = s.size();
    s = ' ' + s;
    ll ans = INF;
    for(ll d=0;d<=25;d++){
        vector<vector<ll>> dp(n+1, vector<ll>(26));
        for(ll i=1;i<=n;i++){
            for(ll p=0;p<=25;p++){
                if(p == s[i]-'a') dp[i][p] = min(dp[i-1][(p-d+26)%26], dp[i-1][(p+d+26)%26]);
                else dp[i][p] = min(dp[i-1][(p-d+26)%26], dp[i-1][(p+d+26)%26]) + 1;
            }
        }
        ans = min(ans, *min_element(dp[n].begin()+1, dp[n].end()));
    }
    print(ans);
    
}
```

# F.红魔馆的微瑕序位

由于要 $S=2$，则最终的排列必须只有两个相邻的数字互换。

假如 $S=0$，则经典结论是 $n-c$，$c$ 为置换换的数量。

假如有 $i$ 和 $i+1$ 属于一个置换环，则可以少一次置换，否则必须先换成 $\texttt{1 2 3 .. n}$ 在交换任意相邻数组。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    vector<ll> vis(n+1), id(n+1);
    ll cnt = 0;
    for(ll i=1;i<=n;i++){
        if(vis[i]) continue;
        cnt++;
        ll cur = i;
        while(!vis[cur]){
            id[cur] = cnt;
            vis[cur] = 1;
            cur = a[cur];
        }
    }
    ll f = 0;
    for(ll i=1;i<n;i++){
        if(id[i] == id[i+1]) f = 1;
    }
    print(n-cnt+(f?-1:1));
}
```

# C++火车头
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
