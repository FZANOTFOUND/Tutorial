# A.ICPC Time

显然答案为  $(n+4) \mod 24$。

时间复杂度 $O(1)$。

```cpp
void solve(){
    print((read()+5)%24);
}
```

# B.倍数

如果数字里有 $0$ 或者 $5$ ，那么把  $0$ 或者 $5$ 放到末尾即可。

时间复杂度 $O(log_{10}n)$。

```cpp
void solve(){
    string s;cin>>s;
    ll f = 0;
    for(auto v:s){
        f|=(v=='5');
        f|=(v=='0');
    }
    cout<<(f?"YES\n":"NO\n");
}
```

# C.邻合

考虑 $dp$。

令 $dp[i][0]$ 为不选择第 $i$ 个数字前 $i$ 个数字可以保留的最大个数，$dp[i][1]$ 为选择第 $i$ 个数字前 $i$ 个数字可以保留的最大个数。

则有
$$
dp[i][0] = max(dp[i-1][0], dp[i-1][1]),
$$

$$
dp[i][1] = \begin{cases}
0  &  a[i] = 1\\
dp[i-1][0] + 1 & a[i] \ne 1 , gcd(a[i], a[i-1])=1\\
max(dp[i-1][0] + 1,dp[i-1][1]+1) & a[i] \ne 1 , gcd(a[i], a[i-1]) \ne 1
\end{cases}
$$

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> a(n+1);
    for(ll i=1;i<=n;i++) a[i] = read();
    vector<PLL> dp(n+1);
    for(ll i=1;i<=n;i++){
        dp[i].fi = max(dp[i-1].fi, dp[i-1].se);
        if(a[i]>1){
            dp[i].se = dp[i-1].fi + 1;
            if(i>1&&__gcd(a[i], a[i-1])>1){
                dp[i].se = max(dp[i].se,dp[i-1].se+1);
            }
        }
    }
    print(n-max(dp[n].fi, dp[n].se));   
}
```

# D.对和

令 $t_i = \lfloor \frac{a_i}{2} \rfloor$  。

则有

$$
\lfloor \frac{a_i + a_j}{2} \rfloor = \begin{cases}
t_i + t_j + 1 & a[i],a[j] 均为奇数\\
t_i + t_j & 其余情况
\end{cases}
$$

设有 $n_1$ 个奇数，奇数的 $t_i$ 之和为 $sum_1$；有 $n_2$ 个偶数，偶数的 $t_i$ 之和为 $sum_2$。则

- 奇数与奇数之间的贡献为 $(n_1-1)*sum_1 + \frac{n_1 * (n_1-1)}{2}$。（后一项为奇数和奇数加起来额外产生的 $1$）
- 偶数与偶数之间的贡献为 $(n_2-1)*sum_2$。

- 奇数与偶数之间的贡献为 $n_1 * sum_2 + n_2 * sum_1$。

时间复杂度 $O(n)$。

```cpp
void solve(){
    ll n = read();
    vector<ll> odd, even;
    ll ans=0, sum1=0, sum2=0;
    for(ll i=1;i<=n;i++){
        ll t = read();
        if(t&1) odd.pb(t),sum1+=t/2;
        else even.pb(t),sum2+=t/2;
    }
    ll n1 = odd.size(), n2 = even.size();
    ans += (n1-1) * sum1 + n1 * (n1-1)/2;
    ans += (n2-1) * sum2;
    ans += n1*sum2 + n2*sum1;
    print(ans);
}
```



# E.镜像

由于 $1\le a, b \le 10^6$，因此我们只需要在$[1, 10^6]$ 的范围内 BFS 即可。

时间复杂度 $O(T*10^6)$

```cpp  
void solve(){
    ll a = read(), b = read(), k = read();
    vector<ll> dis(1e6+1, INF);
    queue<PLL> q;
    q.push({0,a});
    dis[a] = 0;
    while(!q.empty()){
        auto [d,t] = q.front();
        q.pop();
        if(t%10){
            ll tt=0,ttt=t;
            while(ttt){
                tt=(tt*10+ttt%10);
                ttt/=10;
            }
            if(dis[tt]>d+1){
                dis[tt]=d+1;
                q.push({d+1,tt});
            }
        }
        if(t+k<=1e6){
            if(dis[t+k]>d+1){
                dis[t+k]=d+1;
                q.push({d+1,t+k});
            }
        }
    }
    print(dis[b]<INF?dis[b]:-1);
}
```

# F.差异

设 $c_{j}$ 为 $\sum \limits_{i=1}^{n} [s_i[j]==1]$，即所有字符串第 $j$ 个字符 $1$ 的数量之和。

则 
$$
D_i = \sum \limits_{i=1}^{n} \begin{cases}n-c_j & s_i[j] = 1 \\ c_j & s_i[j] = 0\end{cases}
$$
对于第 $j$ 个位置：

- 如果原来为 $1$，则原来不同的数目为 $n-c_j$，变为 $0$ 后 $1$ 的数量减一，不同的数目为 $c_j - 1$，因此 $\Delta_j = 2 * c_j - n - 1$
- 如果原来为 $0$，则原来不同的数目为 $c_j$，变为 $1$ 后 $1$ 的数量加一，不同的数目为 $n-(c_j+1)$，因此 $\Delta_j = n-1-2*c_j$

我们希望最小化不同的数量，即找到一个子数组 $[l_i, r_i] $使得 $\sum \limits_{j=l_i}^{r_i} \Delta_j$ 最小，即最小子数组和。（经典贪心）

答案为 $D_i + min \{\sum \limits_{j=l_i}^{r_i} \Delta_j\}$。

时间复杂度 $O(nm)$。

```cpp
void solve(){
    ll n, m;cin>>n>>m;
    vector<string> s(n);
    vector<ll> cnt(m);
    for(ll i=0;i<n;i++){
        cin>>s[i];
        for(ll j=0;j<m;j++){
            cnt[j] += (s[i][j] == '1');
        }
    }
    for(ll i=0;i<n;i++){
        ll pre = 0;
        for(ll j=0;j<m;j++){
            if(s[i][j] == '1') pre += n-cnt[j];
            else pre += cnt[j];
        }
        vector<ll> d(m);
        for(ll j=0;j<m;j++){
            if(s[i][j] == '1') d[j] = cnt[j]-1 - (n-cnt[j]);
            else d[j] = (n-1-cnt[j]) - cnt[j];
        }
        ll mi = 0, cur = 0;
        for(ll j=0;j<m;j++){
            cur = min(d[j], cur+d[j]);
            mi = min(mi, cur);
        }
        cout<<pre+mi<<'\n';
    }
}
```

