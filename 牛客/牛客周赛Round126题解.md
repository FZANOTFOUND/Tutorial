# A. 小红的顺子构造

显然输出 $\texttt{x x+1 x+2 x+3 x+4}$ 即可。

```py
x = int(input())
print(*range(x, x+5))
```



# B/G.小红的字符串构造

对于 $B$ 按长度排序遍历检查即可。

显然可以使用字典树维护。

在字典树上遍历，若：

- $ tot > k$ 则减去当前字符串的数量，退回上一步
- $tot < k$ 遍历所有可能得下一个字符。
- $tot = k$ 找到答案。

```cpp
struct TrieNode{
    map<char, TrieNode*> children; // 动态开点
    bool isEnd; // 是否为单词的结尾
    bool repeat; //是否出现过
    ll cnt; // 当前前缀对应的字符串出现了几次
    TrieNode(){
        isEnd = repeat = false;
        cnt = 0;
    }
};

class Trie{
    public:
    TrieNode* root;
    Trie(){
        root = new TrieNode();
    }
    
    void insert(const string &s){
        TrieNode * now = root;
        for(char ch:s){
            if(now->children.find(ch)==now->children.end()){
                now->children[ch] = new TrieNode();
            }
            now = now->children[ch];     
        }
        now->cnt++;
        now->isEnd = true;
    }

    PLL find(const string &s){
        TrieNode * now = root;
        for(char ch:s){
            if(now->children.find(ch)==now->children.end()){
                return {0, 0};
            }
            now = now->children[ch];
        }
        if(now->isEnd){
            if(now->repeat){
                return {2, now->cnt};
            }
            now->repeat = 1;
            return {1, now->cnt};
        }
        return {0, 0};
    }
};

void solve(){
    ll n, k;cin>>n>>k;
    Trie trie;
    for(ll i=0;i<n;i++){
        string s;cin>>s;
        trie.insert(s);
    }
    string ans;
    ll tot = 0;
    ll f = 0;
    function<void(TrieNode*, string)> dfs = [&](TrieNode* u, string cur){
        if(f) return;
        tot+=u-> cnt;
        if(tot==k){
            ans=cur;
            f=1;
            return;
        }
        if(tot>k){
            tot-=u->cnt;
            return;
        }
        for(auto[k, v]:u->children){
            dfs(v, cur+k);
            if(f) return;
        }
        tot -= u->cnt;
    };
    dfs(trie.root, "");
    if(f) cout<<ans<<'\n';
    else cout<<"-1\n";
}

int main(){
    fastio;
    init();
    ll t = 1;
    //t = read();
    while(t--){
        solve();
    }
}


```



# C.小红的好数组构造

设出现奇数次的数字的个数为 $x$ ，显然若 $x < k$ ，则可以删除 $x$ 个下标成为好数组，不满足题意。

所以我们构造恰好 $k$ 个数字出现奇数次，此时需要检查剩下的代填数字的个数是不是偶数。

```py
n, k = map(int, input().split())
if n % 2 == k % 2:
    for i in range(k):
        print(i+1, end=' ')
    for i in range(n-k):
        print(k+1, end=' ')
else:
    print(-1)
```



# D.小红的左看右看构造

不难想到可以 $c + max(c) + reverse(d)$。

若 $x + y - 1 > n$ 时，超过 $n$ 个数组。

若 $max(c) \ne max(d)$ 此时两个数组对应的最大值不同，显然不可能构造出来。

```py
x, y, n = map(int, input().split())
c = list(map(int, input().split()))
d = list(map(int, input().split()))
if c[-1] != d[-1] or x + y - 1 > n:
    print(-1)
else:
    print(*(c[:x-1] + [max(c) for i in range(n-x-y+1) ] + d[::-1]))
```

# E.小红的完全平方数构造

显然可以想到遍历后面加了几位。

对于添加了 $k$ 为的情况，此时数字的范围为  $[n \times 10 ^{k},(n+1) \times 10 ^{k}-1]$，不妨取第一个大于等于 $n \times 10 ^{k}$ 的完全平方数，若其小于等于 $(n+1) \times 10 ^{k}-1$ ，则满足题意。

```py
p = [1 for i in range(20)]
for i in range(1, 20):
    p[i] = p[i-1] * 10

def find(x):
    l = 0
    r = 10**10
    ans = -1
    while l <= r:
        mid = (l + r)>>1
        if mid * mid >= x:
            ans = mid
            r = mid - 1
        else:
            l = mid + 1
    return ans

for _ in range(int(input())):
    n = int(input())
    ans = -1
    for i in range(1, 20):
        t = n * p[i]
        res = find(t)
        if res * res <= (n+1)*p[i]-1:
            ans = res*res
            break
    print(ans)
```



# F. 小红的基环树染色构造

可以用 $dfs/bfs$ 找到环。

若环的长度为偶数，则 $ \texttt{1 2  1 2 1 2...1 2}$。

若环的长度为偶数，则 $ \texttt{1 2  1 2 1 2...1 2 3}$。

其余不在环上的点，可以从环上的出发遍历，取不是其父节点的颜色的节点即可。

```cpp
void solve(){
    ll n = read();
    vector<vector<ll>> g(n+1);
    vector<ll> dg(n+1);
    vector<ll> ans(n+1), vis(n+1);
    for(ll i=0;i<n;i++){
        ll u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
        dg[u]++, dg[v]++;
    }
    queue<ll> q;
    for(ll i=1;i<=n;i++){
        if(dg[i] == 1){
            q.push(i);
        }
    }
    while(q.size()){
        auto u = q.front();
        vis[u] = 1;
        q.pop();
        for(auto v:g[u]){
            if(!vis[v]){
                dg[v]--;
                if(dg[v] == 1){
                     q.push(v);
                }    
            }
            
        }
    }
    ll cur = -1;
    for(ll i=1;i<=n;i++){
        if(!vis[i]){
            cur = i;
            break;
        }
    }
    ll pre = 0;
    ll st = cur;
    vector<ll> p;
    do{
        p.pb(cur);
        for(auto v:g[cur]){
            if(ans[v]) continue;
            if(!vis[v]&&v!=pre){
                pre = cur;
                cur = v;
                break;
            }
        }
    }while(st!=cur);
    function<void(ll, ll)> dfs = [&](ll u, ll p){
        
        for(auto v:g[u]){
            if(v == p || ans[v])continue;
            ans[v] = ans[u] % 3 + 1;
            dfs(v, u);
        }
    };

    if(p.size()%2==0){
        for(ll i=0;i<p.size();i++){
            ans[p[i]] = i%2 + 1;
        }
    }
    else{
        for(ll i=0;i<p.size()-1;i++){
            ans[p[i]] = i%2 + 1;
        }
        ans[p.back()] = 3;
    }
    for(auto v:p){
        dfs(v, 0);
    }
    for(ll i=1;i<=n;i++){
        pt(ans[i]), putchar(' ');
    }
}
```

# c++火车头
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
    ll n = read();
    vector<vector<ll>> g(n+1);
    for(ll i=0;i<n-1;i++){
        ll u = read(), v = read();
        g[u].pb(v);
    }
    
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