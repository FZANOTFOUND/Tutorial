# A.小红的图
模拟即可
```py
a, b = map(int, input().split())
ans = ''
if a == 1:
    ans += 'L'
else:
    ans += 'R'
if b == 1:
    ans += 'U'
else:
    ans += 'D'
print(ans)
```

# B.小红的菊花
找度为 $n-1$ 的点即可。

```py
n = int(input())
c = [0 for i in range(n+1)]
for i in range(n-1):
    u, v = map(int, input().split())
    c[u] += 1
    c[v] += 1
for i in range(1, n+1):
    if c[i] == n-1:
        print(i)
```

# C.小红的好矩形
显然要不 $1\times 2$ 要不 $2\times 1$。

方案数即为 $(n-1)*m + (m-1)*n$。

```py
n, m = map(int, input().split())
print(n*(m-1)+m*(n-1))
```

# D.小红嫁接

对于每个邻居至少为 $2$ 个的点，显然除了连接上最后的链的那条边，其余边都需要操作一边。

答案即为总数求和。
```py
n = int(input())
deg = [0 for i in range(n+1)]
for i in range(n-1):
    u, v = map(int, input().split())
    deg[u] += 1
    deg[v] += 1
    
print(sum(max(0, i-2) for i in deg))
```

# E.小红玩马

建图后找最短路，如果距离超出 $k$ 或者和 $k$ 的奇偶性不同，则无法到达。

否则先原地转圈圈即可。

```cpp
vector<PLL> d = {{1, 2},{2, 1},{-1, 2},{2, -1},{-1, -2},{-2, -1},{1, -2},{-2, 1}};
void solve(){
    ll n = read(), m = read(), k = read();
    vector<vector<ll>> g(3*n*m+1);
    function<ll(ll, ll, ll)> encode = [&](ll x, ll y, ll f){
        return ((x-1)*m + y) + n*m*f;
    };
    function<PLL(ll)> decode = [&](ll p){
        if(p > n*m) p -= n*m;
        return PLL{(p-1)/m+1, (p-1)%m+1};
    };
    for(ll i=1;i<=n;i++){
        for(ll j=1;j<=m;j++){
            for(auto [dx, dy]:d){
                ll nx = i + dx, ny = j + dy;
                if(1<=nx&&nx<=n&&1<=ny&&ny<=m){
                    g[encode(i, j, 0)].pb(encode(nx, ny, 1));
                    g[encode(i, j, 1)].pb(encode(nx, ny, 0));
                }
            }
        }
    }
    priority_queue<PLL, vector<PLL>, greater<PLL>> pq;
    vector<ll> dis(3*n*m+1, INF), pre(3*n*m+1, -1);
    ll x1 = read(), y1 = read(), x2 = read(), y2 = read();
    ll s = encode(x1, y1, 0);
    dis[s] = 0;
    pq.push({0, s});
    while(!pq.empty()){
        auto [d, u] = pq.top();
        pq.pop();
        if(d > dis[u]) continue;
        for(auto v:g[u]){
            if(d + 1 < dis[v]){
                pre[v] = u;
                dis[v] = d + 1;
                pq.push({d+1,v});
            }
        }
    }
    ll t = encode(x2, y2, k&1);
    if(dis[t] == 0 && g[s].size()==0){
        puts("No");
        return;
    }
    if(dis[t] <= k){
         
        vector<PLL> ops;
        while(t!=s){
            ops.pb(decode(t));
            t = pre[t];
        }
        if(ops.size()<k){
            PLL ok; 
            if(ops.empty()) {
                if(g[s].empty()){ 
                    puts("No");
                    return;
                }
                ok = decode(g[s][0]);
            } else {
                ok = ops.back(); 
            }
            ll r = k - ops.size();
            while(r){
                ops.pb(decode(s));
                ops.pb(ok);
                r-=2;
            }
        }
         
        reverse(all(ops));
        puts("Yes");
        assert(ops.size()==k);
        for(auto v:ops){
            print(v);
        }
    }
    else{
        puts("No");
    }
     
}
```

# F.小红的⑨
对于每个点，可以分为向下走和向上走两种。

向下走可以有 $u$ 的所有子树少走一步转移得到，即 $down_{u, k} = \sum \limits_{v \in g[u]} down_{v, k-1}$。

向上走即为从 $fa[u]$ 走  $k-1$ 补能走到的点，但是要减去在 $u$ 的子树下的情况，即 $up_{u, k} = up_{fa[u], k-1} + down_{fa[u], k-1} - down_{u, k-2}$。

```cpp
void solve(){
    ll n = read();
    vector<vector<ll>> g(n+1);
    for(ll i=1;i<=n-1;i++){
        ll u = read(), v = read();
        g[u].pb(v);
        g[v].pb(u);
    }
    vector<ll> fa(n+1);
    vector<vector<ll>> down(n+1, vector<ll>(10)), up(n+1, vector<ll>(10));
    function<void(ll, ll)> dfs = [&](ll u, ll p){
        fa[u] = p;
        down[u][0] = 1;
        for(auto v:g[u]){
            if(v == p) continue;
            dfs(v, u);
            for(ll i=0;i<=8;i++){
                down[u][i+1] += down[v][i];
            }
        }
    };
    function<void(ll, ll)> dfs2 = [&](ll u, ll p){
        for(auto v: g[u]){
            if(v == p) continue;
            for(ll d=1;d<=9;d++){
                up[v][d] = up[u][d-1] + down[u][d-1];
                if(d >= 2) up[v][d] -= down[v][d-2];
            }
            dfs2(v, u);
        }
    };
    dfs(1, 0);
    dfs2(1, 0);
    vector<ll> ans(n);
    for(ll i=1;i<=n;i++){
        ans[i-1] = down[i][9] + up[i][9];
    }
    print(ans);
}
```