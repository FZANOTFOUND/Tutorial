# A.小红打怪

显然每次攻击 $r$ 总次数最小，即答案为 $\lceil \frac{a}{r}\rceil$。

```python
a, l, r = map(int, input().split())
print((a+r-1)//r)
```



# B.小红砍怪

注意到只能攻击一次，因此答案为相同的两个数之间的最远距离。

```python
n = int(input())
a = [0] + list(map(int, input().split()))
p = [0 for _ in range(n+1)]
ans = 0
for i in range(1, 2*n+1):
    if not p[a[i]]:
        p[a[i]] = i
    else:
        ans = max(i - p[a[i]] + 1, ans)
print(ans)
```



# C.小红加强打怪

显然，对同一个目标连续攻击到消灭为止最优。

对同一个目标连续攻击 $i$ 次后，总伤害为 $i \times (i+1)$ 。

可以用二分求出每个的最小次数。

```python
n = int(input())
a = list(map(int, input().split()))
ans = 0
for i in a:
    l = 1
    r = 10**18
    tans = -1
    while l <= r:
        mid = (l + r)>>1
        if mid*(mid+1)//2 >= i:
            tans = mid
            r = mid - 1
        else:
            l = mid + 1
    ans += tans
print(ans)
```



# D.小红走迷宫

dfs 或者 bfs 遍历整张图即可。

```cpp
void solve(){
    ll n = read(), m = read(), x = read();
    vector<ll> f(n+1);
    for(ll i=1;i<=x;i++) f[read()] = 1;
    vector<ll> vis(n+1);
    vector<vector<ll>> g(n+1);
    for(ll i=1,u,v;i<=m;i++){
        u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
    }
    function<void(ll, ll)> dfs = [&](ll u, ll p){
        vis[u] = 1;
        for(auto v:g[u]){
            if(v!=p&&!vis[v]&&!f[v]){
                dfs(v, u);
            }
        }
    };
    dfs(1, 0);
    for(ll i=1;i<=n;i++){
        if(vis[i]) pt(i),putchar(' ');
    }
}   
```



# E.小苯的刷怪笼

每次攻击最多使得奇数位上的数字 $-1$ ，偶数位上的数字 $-1$，因此不难得出对一个序列 $ans$，最小攻击次数为奇数位之和和偶数位之和的最小值，因此 $a-k \le k $。

同时，因为小红一定优先两两攻击，则我们让除了第一个数之外全是 $1$，最多可以让小红攻击 $ a - \lfloor \frac{n}{2} \rfloor$ 次。

因此 $k$ 满足 $ \lceil \frac{a}{2} \rceil \le k \le a - \lfloor \frac{n}{2} \rfloor$，否则为 $-1$。

我们只要让奇数位之和为 $k$ ，偶数位之和为 $a-k$ 即可。

注意特判 $n = 1$。

```cpp
void solve(){
    ll n = read(), a = read(), k = read();
    if(n == 1){
        if(a == k){
            print(a);
        }
        else{
            print(-1);
        }
        return;
    }
    if(!((a+1)/2<=k&&k<=(a-n/2))){
        print(-1);
        return ;
    }
    vector<ll> ans(n, 1);
    ans[0] += k - (n+1)/2;
    ans[1] += (a-k) - (n/2);
    print(ans);
}   
```



# F.毒苯

不难想到用并查集模拟，但是在线写时间复杂度 $O(qnm)$。如果预处理了空间复杂度至少 $O(n^2m^2)$ （$nm$个并查集）。

因此考虑离线处理。

我们从小大大排列所有点和询问。对每个询问 $q$ 把所有值不超过 $q$ 的点加入并查集并与四周链接。

注意我们没法每次询问都找一遍第一行的元素（个人感觉每次找一遍容易卡常），因此对每个连通分量我们要记录其与第一行有没有链接，并且每次链接点的时候记录变化值。

```cpp
class DSU{
    public:
    vector<ll> parent, size, flag;
    DSU(ll n){
        parent.resize(n+1);
        size.resize(n+1, 1);
        flag.resize(n+1);
        for(ll i=1;i<=n;i++) parent[i] = i;
    }
    ll find(ll p){
        if(parent[p]!=p)parent[p]=find(parent[p]);
        return parent[p];
    }
    ll unite(ll u, ll v){
        u = find(u), v = find(v);
        if(u == v) return 0;
        if(size[u]<size[v]) swap(u, v);
        ll pre = flag[u] * size[u] + flag[v] * size[v];
        parent[v] = u;
        size[u] += size[v];
        flag[u]|=flag[v];
        ll now = flag[u] * size[u];
        return now - pre;
    }
};
vector<PLL> d = {{1, 0}, {-1, 0}, {0, -1},{0, 1}};

void solve(){
    ll n = read(), m = read(), q = read();
    vector<vector<ll>> a(n+1, vector<ll>(m+1));
    vector<PLL> ps;
    ll idx = 1;
    auto trans = [&](ll x, ll y){
        return (x-1) * m + y;
    };
    for(ll i=1;i<=n;i++){
        for(ll j=1;j<=m;j++){
            a[i][j] = read();
            ps.pb({a[i][j], trans(i, j)});
        }
    }
    vector<PLL> qs;
    vector<ll> ans(q);
    for(ll i=0;i<q;i++){
        qs.pb({read(), i});
    }
    
    DSU dsu((n+2)*(m+2));
    for(ll y=1;y<=m;y++) dsu.flag[trans(1, y)] = 1;
    sort(all(qs));
    sort(all(ps));
    ll idxp = 0;
    ll res = 0;
    vector<vector<ll>> vis(n+2, vector<ll>(m+2));
    for(auto [qx, idx]:qs){
        while(idxp<ps.size()&&ps[idxp].fi<=qx){
            ll x = (ps[idxp].se-1)/m + 1, y = (ps[idxp].se-1) % m + 1;
            vis[x][y] = 1;
            if(x == 1) res++;
            for(auto [dx, dy]:d){
                ll nx = x + dx, ny = dy + y;
                if(1<=nx&&nx<=n&&1<=ny&&ny<=m&&a[nx][ny]<=qx&&vis[nx][ny]){
                   res += dsu.unite(ps[idxp].se, trans(nx, ny));
                }
            }
            ++idxp;
        }
        ans[idx] = res;
    }
    for(ll i=0;i<q;i++) print(ans[i]);
    
}   
```

