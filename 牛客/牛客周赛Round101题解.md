~~76真坏，让我的F红红的~~

![红红的](https://uploadfiles.nowcoder.com/images/20250720/226800108_1753018791969/B5A8F50995101DD210CBC5C11D77DD10)

# A.题解的token计算

按题意输出即可

```cpp
void solve(){
    ll n;cin>>n;
    cout<<fixed<<setprecision(12)<<150*1.0*log(n)<<'\n';
}

```

# B.76修地铁

按题意$O(n)$模拟即可。

```cpp
void solve(){
    ll c1 = 0, c2 = 0, c3 = 0, c4 = 0;
    ll n;cin>>n;
    for(ll i=1;i<=n;i++){
        if (i % 5 == 0)c1 += 2;
        if (i % 10 == 5)c2 += 1;
        if (i % 20 == 0)c3 += 3;
        else c4 += 2;
    }
    cout<<c1<<' '<<c2<<' '<<c3<<' '<<c4<<'\n';
}
```



# C.76选数

要最大化异或和，可以想到把每一位全部变成 $1$。

对于 $n$, 存在一个比 $n$ 小的数字使得异或和全部是  $1$。

例如对于 $4$ ，取 $3$，可以使得 $4$ 的每一位二进制都变成 $1$。

又因为无法把 $n$的更高位变成 $1$，因此答案就是把 $n$ 的每一位变成 $1$。

```cpp
void solve(){
    ll n;cin>>n;
    cout<<((1ll<<(__lg(n)+1))-1)<<'\n';
}
```



# D.76构造

注意到一定有一段区间元素的 $gcd$ 为 $1$。（包含 $1$ 的那一段）

所以如果 $m$ 为偶数，一定不可能。

$m$ 为奇数时，我们可以让 $m$ 中除 $1$ 外每个二进制位为单独的一段区间。剩下的数字中一定有 $1$， $gcd$ 一定为 $1$。

例如 $n= 6, m = 7$ 时 我们把 $2$ 、$4$ 作为单独的区间，剩下的数字 $1, 3, 5, 6$ 作为另一个区间。

如果$m$ 中有一位二进制的大小超过 $n$ ，则这位二进制无法被构造出来，此时不可能。

注意边界特判。

```py
void solve(){
    ll n = read(), m = read();
    if(n == 1){
        if(m==1){
            puts("1\n1\n1 1");
        }
        else{
            puts("-1");
        }
        return;
    }
    if(n==2&&m==1){
        puts("1 2\n1\n1 2");
        return;
    }
    if(m%2==0){
        puts("-1");
        return;
    }
    vector<ll> p, f(n+1);
    ll cnt = 0;
    for(ll bit=63;bit>=1;bit--){
        if((m>>bit)&1){
            if((1ll<<bit)>n){
                puts("-1");
                return;
            }
            cnt++;
            p.pb(1ll<<bit);
            f[1ll<<bit] = 1;
        }
    }
    for(ll i=1;i<=n;i++){
        if(!f[i]) p.pb(i);
    }
    for(ll i=0;i<n;i++){
        pt(p[i]),putchar(i==n-1?'\n':' ');
    }
    vector<PLL> ops;
    for(ll i=1;i<=cnt;i++){
        ops.pb({i, i});
    }
    if (cnt < n)
        ops.pb({cnt+1, n});
    pt(ops.size()),puts("");
    for(auto [l, r]:ops){
        pt(l),putchar(' '),pt(r), puts("");
    }
}
```





# E.qcjj寄快递

~~高中数学题~~


以下过程中为区分距离和自然常数，设距离为 $m$。

令 $f(x) = 2x + \frac{2m}{2^x}(x\ge0)$，则 $f^{'}(x) = 2 -  2mln2\cdot 2^{-x} $

$f^{'}(x) = 0 $ 时，$x =log_{2}(mln2)$ 。且 $x>log_{2}(mln2)$ 时 $f^{'}(x) >0$

因为 $x\ge0$ ,所以 $log_{2}(mln2) <0$ 时，即 $mln2<1$时，取 $x=0$

带入原式得:

$mln2<1$时， $f_{min} = 2m$

$mln2 \ge 1$时， $f_{min} = 2log_{2}(mln2)+ \frac{2}{ln2}$

$mln2<1$图：

![mln2<1](https://uploadfiles.nowcoder.com/images/20250720/226800108_1753018830574/54CE63B3B50F2F2ABFF0F59582CD92C9)


$mln2>=1$图：

![mln2 \ge 1](https://uploadfiles.nowcoder.com/images/20250720/226800108_1753018838978/EDC9B0F4EF8F6F42683AC4FC0BA1BE64)


```cpp
void solve() {
    ll n;cin>>n;
    vector<pair<db, db>> p(n+1);
    for(ll i=1;i<=n;i++) cin>>p[i].fi>>p[i].se;
    db ans = 0;
    for(ll i=1;i<n;i++){
        auto [x1, y1] = p[i];
        auto [x2, y2] = p[i+1];
        db m = sqrtl(pow(x1-x2, 2)+pow(y1-y2, 2));
        db x = log2(m * log(2));
        if (m * log(2) > 1){
            ans += 2 * x + 2 * m/pow(2, x);
        }
        else{
            ans += 2 * m;
        }
    }
    cout<<fixed<<setprecision(12)<<ans<<'\n';
}
```



# F. 幂中幂plus

由于 $MOD \le 10^6$ ，因此 $c_i$ 最多有 $10^6$ 个取值，必定存在循环节。

由于循环节不可能超过 $10^6$，可以暴力求出循环节。

具体为，不断循环直到出现重复数字，此时就找到了循环节。

找到循环节后就可以 $O(1)$ 回答每个询问。

注意 $c_0$ 可能很大，快速幂不要爆 $ll$ 以及 指数为$0$ 要返回 $1$。



```cpp
void solve(){
    ll b = read(), c0 = read();
    MOD = read();
    if(MOD == 1){
        ll q = read();
        while(q--){
            print(0);
        }
        return;
    }
    vector<ll> memo(MOD+1, -1);
    ll c = ksm(b, c0), cnt=0;
    vector<ll> pre(1, 0);
    while(memo[c]==-1){
        cnt++;
        memo[c] = cnt;
        pre.pb((pre.back()+c)%MOD);
        c = ksm(b, c);
    }
    ll len = cnt - memo[c] + 1;
    ll su = (pre[cnt]-pre[memo[c]-1]+MOD)%MOD;
    ll q = read();
    while(q--){
        ll k = read();
        if (k <= cnt){
            print(pre[k]%MOD);
        }
        else{
            ll t = (k -memo[c] + 1)/len%MOD;
            ll ans = t * su % MOD;
            ans = (ans + pre[memo[c]-1])%MOD;
            ll r = (k - memo[c] + 1)%len;
            ans = (ans + pre[memo[c]-1+r]-pre[memo[c]-1]+MOD)%MOD;
            print(ans);
        }
    }
}
```