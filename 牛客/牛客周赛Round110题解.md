# A.小苯的数字染色
易得由 $2$, $3$ 无法表示的数字有且仅有 $1$。因此除了 $1$ 之外的所有数字都可以。

时间复杂度 $O(1)$。


``` cpp
void solve(){
    puts(read()>=2?"YES":"NO");
}    
```

# B.小苯的数组重排

~~赛时的数据疑似 $1\le a_i \le 10^9$，攻击出题人后现在应该已经改成 $1\le a_i \le 10^5$ 了~~

原式显然可以化成 $ 2 \times \sum \limits_{i=1}^{n} a_i - a_1 - a_n$。

因此只需让 $a_1, a_n$ 为最小的两个数字就行了。

时间复杂度 $O(nlogn)$。

``` cpp
void solve(){
    ll n = read();
    vector<ll> a(n);
    for(ll i=0;i<n;i++) a[i] = read();
    sort(all(a));
    ll ans = a[0] + a[1] + accumulate(a.begin()+2, a.end(), 0ll) * 2;
    print(ans);
}   
```

# C.小苯的麦克斯

对于包含最大值的一个长度为 $2$ 的子数组，不难发现往其中添加数字是不优的（会使答案减小或不变）。

因此只需检查最大值和周围元素组成的字数组即可。

时间复杂度 $O(n)$。


``` cpp
ll mex(ll a, ll b){
    if(a > b) swap(a, b);
    ll v = 0;
    if(a == v) v++;
    if(b == v) v++;
    return v;
}
void solve(){
    ll n = read();
    vector<ll> a(n);
    for(ll i=0;i<n;i++) a[i] = read();
    ll mx = *max_element(all(a));
    ll mxa = -INF;
    for(ll i=0;i<n;i++){
        if(a[i] == mx){
            if(i){
                mxa = max(mxa, mx - mex(mx, a[i-1]));
            }
            if(i < n-1){
                mxa = max(mxa, mx - mex(mx, a[i+1]));
            }
        }
    }
    print(mxa);
}   
```

# D.小苯的平衡序列
遍历每个数，计算剩下的数字的中位数，把原式拆成两部分计算即可。

可以用 $\texttt{__gnu_pbds::tree}$ 或者双堆实现。

时间复杂度 $O(nlogn)$。

``` cpp
class DS{
    public:
    ll t1,t2;
    DS(){
        t1 = t2 = 0;
    }
    multiset<ll> q1,q2;
    void clr(){
        q1.clear();
        q2.clear();
        t1=t2=0;
    }
    void remake(){
        while(q1.size()>q2.size()) q2.insert(*q1.rbegin()),t1-=*q1.rbegin(),t2+=*q1.rbegin(),q1.erase(--q1.end());
        while(q1.size()<q2.size()) q1.insert(*q2.begin()),t1+=*q2.begin(),t2-=*q2.begin(),q2.erase(q2.begin());
    }
    void add(ll x){
        q1.insert(x);t1+=x;
        remake();
    }
    void del(ll x){
        if(q1.find(x)!=q1.end()) q1.erase(q1.lower_bound(x)),t1-=x;
        else q2.erase(q2.lower_bound(x)),t2-=x;
        remake();
    }
    ll qry(){
        if(q1.empty()) return 0ll;
        return ll(q1.size())**q1.rbegin()-t1+t2-ll(q2.size())**q1.rbegin();
    }
};
 
void solve(){
    ll n = read();
    DS ds;
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++){
        a[i] = read();
        ds.add(a[i]);
    }
    ll mi = INF;
    for(ll i=1;i<=n;i++){
        ds.del(a[i]);
        mi = min(mi, ds.qry());
        ds.add(a[i]);
    }
    print(mi);
     
}   
```

# E.小苯的数字变换
手玩一下可得 $f(x) = (x-1)\%9+1$。

特例是  $x=0$ 时 $f(x) = 0$。

可以使用前缀和去枚举每个区间（前缀和对 $9$ 取模）。

注意要处理区间是全 $0$ 的情况，因此统计每个前缀和出现几次时，先加到 $temp$ 上，遇到非 $0$ 数字再加回 $cnt$ 中。


``` cpp
void solve(){
    string s;cin>>s;
    ll n = s.size();
    s = " " + s;
    vector<ll> pre(s.size());
    vector<ll> cnt(10);
    cnt[0] ++;
    ll ans = 0;
    vector<vector<ll>> pos(10);
    vector<ll> temp(10);
    for(ll i=1;i<=n;i++){
        if (s[i] != '0') {
            for (ll j = 0 ; j <= 9; j++) {
                cnt[j] += temp[j];
                temp[j] = 0;
            }
        }
        pre[i] = (pre[i-1] + s[i]-'0')%9;
        for(ll j=0;j<=9;j++) {
            ll t = (pre[i] - j+18-1)%9+1;
            ans += t * cnt[j];
        }
        temp[pre[i]]++;
    }
     
    cout<<ans<<'\n';
     
}   
```

# F.小苯的序列合并

考虑只有三个 $0$ 或 $1$ 的情况。

可以发现有一个 $1$ 和两个 $0$ 的时候，所有数字异或起来答案会变大。

其余情况答案不变。


因此当数组中元素大于 $3$ 个时，我们一定能选出三个数字异或后答案不会减小，即最后会剩下一个或者两个数字。

因此我们只需要遍历每个分割点统计最大答案即可。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1), pre(n+2), surf(n+2);
    for(ll i=1;i<=n;i++){
        a[i] = read();
        pre[i] = pre[i-1] ^ a[i];
    }
    for(ll i=n;i>=1;i--){
        surf[i] = surf[i+1] ^ a[i];
    }
     
    surf[n+1] = (1ll<<60)-1;
    ll ans = 0;
    for(ll i=1;i<=n;i++){
        ans = max(ans, pre[i]&surf[i+1]);
    }
    print(ans);
     
}  
```

火车头参考
```cpp
// FZANOTFOUND
#include <bits/stdc++.h>
using namespace std;

#define pb push_back 
#define eb emplace_back 
#define fi first
#define se second
#define sep "======"
#define fastio ios::sync_with_stdio(false);cin.tie(0);
#define all(a) a.begin(), a.end()

typedef long long ll;
typedef unsigned long long ull;
typedef long double ld;
typedef pair<long long,long long> PLL;
typedef tuple<ll,ll,ll> TLLL;
const ll INF = (ll)2e18+9;
//const ll MOD = 1000000007;
const ll MOD = 998244353;
const ld PI = 3.14159265358979323;

//io functions
inline void rd(ll &x){x=0;short f=1;char c=getchar();while((c<'0'||c>'9')&&c!='-') c=getchar();if(c=='-') f=-1,c=getchar();while(c>='0'&&c<='9') x=x*10+c-'0',c=getchar();x*=f;}  
inline ll read(){ll x=0;short f=1;char c=getchar();while((c<'0'||c>'9')&&c!='-') c=getchar();if(c=='-') f=-1,c=getchar();while(c>='0'&&c<='9') x=x*10+c-'0',c=getchar();x*=f;return x;}  
inline void pt(ll x){if(x<0) putchar('-'),x=-x;if(x>9) pt(x/10);putchar(x%10+'0');}
inline void print(ll x){pt(x), puts("");}
inline void print(PLL x){pt(x.fi), putchar(' '), pt(x.se), putchar('\n');}
inline void print(vector<ll> &vec){for(const auto t:vec)pt(t),putchar(' ');puts("");}
inline void print(const map<ll, ll>& g) {for(const auto& [key, value]:g){cout<<"key: "<<key<<" -> "<<value<<" ";}puts("");}
inline void print(vector<PLL> &vec){puts(sep);for(const auto v:vec){print(v);}puts(sep);}
inline void print(const map<ll, vector<ll>>& g) {for (const auto& [key, value] : g) { cout << "key: " << key << " -> ";for (const auto& v : value) {cout << v << " ";}cout << endl;}}

//fast pow
ll ksm(ll a, ll b=MOD-2,ll mod=MOD){a%=mod;ll res = 1;while(b){if(b&1){res=(res*a)%mod;}a=(a*a)%mod;b>>=1;}return res;}

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