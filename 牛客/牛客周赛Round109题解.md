# A. 小红的直角三角形
显然两个点一个在 $x$ 轴上，另一个在 $y$ 轴上时满足条件。

时间复杂度 $O(1)$。

``` py
a,b,c,d=map(int,input().split())
if (a==0 and d== 0) or (c==0 and b==0):
    print("Yes")
else:
    print("No")
```

# B.小红的好点对
对每个点检查四个方向有没有点即可，最后答案再除 $2$ 去掉重复统计。

时间复杂度 $O(n)$。

也可以遍历每个点对，检查距离是否为 $1$。

时间复杂度 $O(n^2)$。
```python []
# O(n)
n = int(input())
p = [list(map(int, input().split())) for i in range(n)]
memo = {tuple(i) for i in p}
ans = 0
for x, y in p:
    for dx, dy in [[1, 0],[-1, 0], [0, 1], [0, -1]]:
        if (x+dx, y+dy) in memo:
            ans += 1
print(ans//2)
```
```python []
# O(n^2)
n = int(input())
p = [list(map(int, input().split())) for i in range(n)]
ans = 0
for i in range(n):
    for j in range(i):
        x1, y1 = p[i]
        x2 , y2 = p[j]
        if (x1-x2)**2 + (y1-y2)**2 == 1:
            ans += 1
print(ans)
```
# C. 小红的整数三角形

考虑构造直角三角形。

为了使得面积是整数，可以让另一条边扩大一倍。

时间复杂度 $O(n)$。

``` py
x1, y1, x2 , y2 = map(int, input().split())
x = x2 + 2 * y2 - 2 * y1
y = y2 + 2 * x1 - 2 * x2
print(x, y)
```

# D.小红的马

不防考虑每个兵可以被哪些位置的马攻击。

可以发现点图和马可以攻击的点图是一样的。

那么就可以统计所有兵周围的 $8$ 个点，再找最大的点即可。

时间复杂度 $O(n)$。

``` py
from collections import defaultdict
n = int(input())
memo = defaultdict(int)
vv = set()
for _ in range(n):
    x, y=  map(int, input().split())
    vv.add((x, y))
for x, y in vv:
    for dx, dy in [(-1, -2), (1, 2), (1, -2), (-1, 2)]:
        
        if (x+dx, y + dy) not in vv and x + dx > 0 and y + dy > 0:
            memo[(x+dx, y+dy)]+=1
        if (x + dy, y + dx) not in vv and x + dy > 0 and y + dx > 0:
            memo[(x+dy, y+dx)] += 1
mx = max(memo.values())
for k in memo:
    if memo[k] == mx:
        print(*k)
        break
```

# E.小红的好矩形
不难发现，我们可以考虑相邻的 $x$ 和 $y$。

具体的，对每个 $x = k$ 的点 ，检查和 $x = k +1$ 的点 $y$ 相同的点。

如果有 $cnt$ 个，则对答案的贡献为 $\frac{cnt*(cnt-1)}{2}$。

对 $y$ 同理。但注意长和宽均为 $1$ 的矩形会被统计两次，要注意去重。

时间复杂度 $O(nlogn)$。

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<ll, ll>PLL;
#define fi first
#define se second
#define pb push_back
int main(){
    ios::sync_with_stdio(false);
    cin.tie(0), cout.tie(0);
    ll n;cin>>n;
    vector<PLL> p(n);
    for(ll i=0;i<n;i++) cin >> p[i].fi >> p[i].se;
    map<ll, map<ll, ll>> xs, ys;
    for(auto [x, y]:p){
        xs[x][y] = 1;
        ys[y][x] = 1;
    }
    ll ans = 0;
    for(auto [k, v]:xs){
        ll cnt = 0;
        for(auto [vv, _]:v){
            if(xs.contains(k+1)&&xs[k+1].contains(vv)){
                cnt++;
            }
        }
        ans += (cnt-1)*cnt/2;
    }
    for(auto [k, v]:ys){
        vector<ll> memo;
        for(auto [vv, _]:v){
            if(ys.contains(k+1)&&ys[k+1].contains(vv)){
                memo.pb(vv);
            }
        }
        ll t = memo.size();
        ll tt = t * (t-1)/2;
        for(ll i=1;i<memo.size();i++){
            if (memo[i]-memo[i-1]==1){
                tt--;
            }
        }
        ans += tt;
    }
    cout<<ans<<'\n';
}
```

# F.小红的线下查询

注意到要求可以转化为：
$$
\begin{cases}
u = y - x \leq k_1 \\
v = y + x \leq k_2
\end{cases}
$$

所以可以转化为二维数点问题离线处理。

对所有点按 $ u $ 升序排序，对所有查询按 $k_1$ 升序排序。

对每个查询，先把 $u<k_1$ 的所有点的 $v$ 加入树状数组中，在查询小于 $k_2$ 的点有几个。

数据范围大，需要先离散化。

时间复杂度 $O((n+q)log(n+q))$

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef pair<ll, ll>PLL;
#define fi first
#define se second
#define pb push_back
#define all(x) x.begin(), x.end()
class BIT{
    public:
    vector<ll> c;
    ll n;
    BIT(ll n_){
        n = n_;
        c.resize(n+1);
    }
    void add(ll x, ll d){
        for(;x<=n;x+=(x&-x)) c[x] += d;
    }
    ll query(ll x){
        if(x <= 0) return 0;
        ll res = 0;
        for(;x;x-=(x&-x)) res += c[x];
        return res;
    }
};
    
int main(){
    ios::sync_with_stdio(false);
    cin.tie(0), cout.tie(0);
    ll n, q;cin>>n>>q;
    vector<array<ll,4>> tot;
    vector<ll> pp;
    for(ll i=0;i<n;i++){
        ll x, y;cin>>x>>y;
        tot.pb({y-x, y+x, 0, i});
        pp.pb({y-x});
        pp.pb({y+x});
    }
    for(ll i=0;i<q;i++){
        ll k1, k2;cin>>k1>>k2;
        tot.pb({k1, k2, 1, i});
        pp.pb(k1);
        pp.pb(k2);
    }
    vector<ll> ans(q);
    sort(all(tot), [&](array<ll, 4> &x, array<ll, 4> & y){
        if(x[0]!=y[0]){
           return x[0]<y[0];
        }
        
        if(x[2]!=y[2]){
            return x[2]>y[2];
        }
        return x[1]<y[1];
    });
    map<ll, ll> name, back;
    ll idx = 1;
    sort(all(pp));
    for(auto v:pp){
        if(!name[v]){
            name[v] = idx;
            back[idx] = v;
            idx++;
        }
    }   
    BIT bit((ll)4e5+7);
    ll res = 0;
    for(auto [x, y, t, idx]:tot){
        if(t == 1){
            ans[idx] = bit.query(name[y]-1);
        }
        else{
            bit.add(name[y], 1);
        }
    }
    for(auto v:ans){
        cout<<v<<'\n';
    }
        
}

```                        