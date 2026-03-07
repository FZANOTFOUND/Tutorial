# A.ICPC Penalty


按题意模拟即可

~~（一个血的教训：判断字符串是那种可以只判断第一个字母（如果没有重复，否则全打打错了就寄了，某人Unknown打错过）~~

```py
s = input()
n, t = map(int, input().split())
if s[0] == "A":
    print((n-1)*20+t)
else:
    print(0)
```



# B.小苯的无限数组

显然每次操作后 $a_n$ 会变为 $2*a_n$。

答案即为 $a_n * 2^k$。

```py
for _ in range(int(input())):
    n, k = map(int, input().split())
    print(n*(1<<k))
```



# C.小苯的真假游戏

由于是环形的，不难想到最多只有两种答案。

设 $pre$ 为上一个人说真假的情况。若 $s_i$ 为 $1$， 则 $pre$ 不变；若 $s_i$ 为 $0$，则 $pre$ $01$ 翻转（$1->0, 0->1$)。

因此整个过程中 $pre$ 会翻转 $cnt_0$（字符串中 $0$ 的个数） 次。要合法必须满足转一圈后 $pre$ 不变，因此 $cnt_0$ 必须为偶数。



```py
for _ in range(int(input())):
    n = int(input())
    s = input()
    if s.count("0") % 2 == 0:
        print(2)
    else:
        print(0)
```



# D. 小苯的区间选数2.0

经典贪心题。

按左端点排序后，对于当前 $mex$ 将所有左端点小于其的区间的右端点插入优先队列中，在从中取出至少为 $mex$ 的最小数字即可。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define fi first
#define se second
int main(){
    ios::sync_with_stdio(false);
    cin.tie(0), cout.tie(0);
    int t;cin>>t;
    while(t--){
        ll n;cin>>n;
        vector<pair<ll, ll>> memo(n);
        for(ll i=0;i<n;i++) cin>>memo[i].fi>>memo[i].se;
        sort(memo.begin(), memo.end());
        priority_queue<ll, vector<ll>, greater<ll>> pq;
        ll mex = 0, idx=0;
        while(1){
            while(idx<n&&memo[idx].fi<=mex){ // 添加所有左端点 <= mex 的区间
                pq.push(memo[idx].se);
                idx++;
            }
            while(pq.size()&&pq.top()<mex) pq.pop();// 选取右端点 >= mex 的最小右端点
            if(pq.empty()) break; // 如果没有右端点了，意味着枚举完了，退出循环
            pq.pop();
            mex++;
        }
        cout<<mex<<'\n';
    }
}
```

# E.小苯的GCD疑问1.0

结论题：最优解即为选取所有数字。

证明：

- 区间长度为 $1$ 时，显然必须选择所有数字。

- 区间长度不为 $1$ 时，最优解为选择所有数字，此时 $gcd = 1$。

$gcd \ne 1$ 时，由于**最大值被删去**，所有选择的数字的 $gcd$ <  从选择的数字出发连续 $gcd$ 个数字的和。
        

以 $l = 2, r = 8$ 为例。
        

- 若 $gcd = 1$，即为选取所有数字， 有贡献的数字为$\texttt{2 3 4 5 6 7}$。
  
- 若 $gcd = 2$ ，有贡献的数字为 $\texttt{2 4 6}$，对于$2$ ，$2*2 < 2 + 3$ , $\texttt{4 6}$ 同理。
  
- 若 $gcd = 3$ , 有贡献的数字为 $\texttt{3}$，对于$3$ ，$3*3 < 3 + 4 + 5$。
        

以此类推可以发现 $gcd != 1$ 的方案总是小于 $gcd = 1$ 的情况。

求和公式 $O(1)$ 回答即可。


**鞭尸**

本题答案可以到 $1e18$, 有人试图 $\texttt{print(int(2*(L+R-1)*(R-L)/4))}$ 或者 $\texttt{print(int((L+R-1)*(R-L)/2))}$ 是会爆精度的喵~。

例如 $ l = 103593486$  , $r = 472977664$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define fi first
#define se second
int main(){
    ios::sync_with_stdio(false);
    cin.tie(0), cout.tie(0);
    int t;cin>>t;
    while(t--){
        ll l, r, k;cin>>l>>r>>k;
        cout<<(l+r-1)*(r-l)/2<<'\n';
    }
}
```



# F.小苯的GCD疑问2.0

**注意由于最大值没有去掉，$E$ 的结论不适用**

数论分块板题。

显然我们会选取尽可能多的 $gcd$ 相同的数字。

对于选取数字数量相同的 $gcd$ 区间 $[l, r]$ ，显然此时选择 $gcd = r$  的答案最大。

于是分块选取每个右端点，$O(\sqrt n)$ 枚举即可。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define fi first
#define se second
int main(){
    ios::sync_with_stdio(false);
    cin.tie(0), cout.tie(0);
    int t;cin>>t;
    while(t--){
        ll n, k;cin>>n>>k;
        ll l = 1;
        ll ans = 0;
        while(l <= n){
            ll r = min(n, n/(n/l));
            ll cnt = n/l;
            if(cnt < k) break;
            ans = max(ans, (r + cnt*r) * cnt/2 * r);
            l = r + 1;
        }
        cout<<ans<<'\n';
    }
}
```