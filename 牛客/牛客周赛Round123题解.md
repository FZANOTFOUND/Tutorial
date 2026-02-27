# A.小红玩牌

按题意模拟即可。

```py
n, c = input().split()
nn, cc = input().split()
if int(n) != int(nn):
    print("Yes" if int(n) > int(nn) else "No")
else:
    print("Yes"  if c < cc else "No")
```

# B.小红作弊

  显然对于总和超出四张的牌需要进行一次操作。

```py
a = list(map(int, input().split()))
b = list(map(int, input().split()))
cnt = 0
for i in range(13):
    cnt += max(a[i] + b[i] - 4 , 0)
print(cnt)
```

# C.小红出对

对牌去重后，按同一个花色匹配即可。

注意输出的是打出的牌数而不是对数。

```py
n = int(input())
memo = [[0 for i in range(4)] for i in range(2*10**5+1)]

for i in range(n):
    n, c = input().split()
    n = int(n)
    c = ord(c) - ord('A')
    memo[n][c] = i + 1
ans = []
for i in range(1, 2*10**5+1):
    ok = []
    for j in range(4):
        if memo[i][j]:
            ok.append(memo[i][j])
    for j in range(0, len(ok)-1, 2):
        ans.append([ok[j], ok[j+1]])
print(len(ans)*2)
for i in ans:
    print(*i)
```



# D. 小红打牌

首先枚举所有满足 $cnt_i , cnt_{i+1}  \ge 3 $ 的 $i$ ，接下来的两对分**$4$ 张一样的牌**和 **$2$ 组  $2$ 张一样的牌**两种情况。

注意对于 $i$ 和 $i+1$，计算其是否可以作为一对存在时要去掉 $3$ 张牌。

```py
MOD = 998244353
n = int(input())
a = list(map(int, input().split()))
cnt = [0 for i in range(2*10**5+1)]
for i in a:
    cnt[i] += 1
pre = [0 for i in range(2*10**5+1)]
pre2 = [0 for i in range(2*10**5+1)]
for i in range(1, 2*10**5+1):
    pre[i] = pre[i-1] + (cnt[i] >= 2)
    pre2[i] = pre2[i-1] + (cnt[i] >= 4)
ans = 0
for i in range(1, 2*10**5):
    if cnt[i] >= 3 and cnt[i+1] >= 3:
        res = (pre[i-1] + pre[2*10**5]-pre[i+1] + (cnt[i]>=5) + (cnt[i+1]>=5) + MOD)%MOD
        ans = (ans + res % MOD * (res-1)//2%MOD)%MOD
        ans += (pre2[i-1] + pre2[2*10**5]-pre2[i+1]+ (cnt[i]>=7) + (cnt[i+1]>=7) + MOD)%MOD;
print(ans)
```



# E/F.小红出牌

对于 $E$ :

不妨考虑添加一张牌 $i$ 对顺子数量的变化。

如果  $i-1, i+1$ 都不存在，则顺子数量 $+ 1$。

如果存在一个 ，则顺子数量不变。

如果都存在，两段合成一段，顺子数量 $-1$。

于是可以发现 $ \Delta = 1 - [cnt_{i-1} > 0] - [cnt_{i+1} > 0]$

对于 $F$ :

扩展 $E$ 中的结论，不难发现我们考虑的是 $i-1$ 和 $i+1$ 是否存在了至少 $cnt_i + 1$ 个。

则 $ \Delta = 1 - [cnt_{i-1} > cnt_i] - [cnt_{i+1} > cnt_i]$

```py
n = int(input())
a = [0] + list(map(int, input().split()))
cnt = [0 for i in range(n+2)]
ans = [0]
for i in range(1, n+1):
    ans.append(ans[-1] + 1 - (cnt[a[i]-1]>cnt[a[i]]) - (cnt[a[i]+1]>cnt[a[i]]))
    cnt[a[i]] += 1
print(*ans[1:])
```

# G.小红出千

显然我们可以选择一段长度为 $n$ 的区间，使得 $[l, l+n-1]$ 内不重复的数字的数量最大。

可以用滑动窗口实现。

接下来，注意到我们可以变化的 $x$ 的范围为 $1 \leq x \leq 2 \times 10^9$，而 $1\leq a_i \leq 10^9$ ，所以从 $l$ 开始填数字即可。

注意对于 $[l, l+n-1]$ 内的数字，第一次可以保持不动，以后仍然需要移动。

```py
from collections import defaultdict
n = int(input())
a = list(map(int, input().split()))
b = a[:]
a = list(sorted(set(a)))
segs = []
l = 0
mx = 0
k = []
for r in range(len(a)):
    while a[r] - a[l] > n - 1:
        l += 1
    if r - l + 1 > mx:
        mx = r - l + 1
        k = [a[l], a[r]]

l, r = k
r = l + n - 1
ops = []
has = defaultdict(int) # 数字是否已经有了
memo = defaultdict(int) # 用于判断 [l, l+n-1] 内的数字是不是第一次出现
for i in b:
    if l <= i <= r:
        has[i] = 1
cur = l
for i in range(len(b)):
    if l <= b[i] <= r:
        if memo[b[i]]:
            while has[cur]:
                cur += 1
            ops.append([i+1, cur])
            has[cur] = 1
    else:
        while has[cur]:
            cur += 1
        ops.append([i+1, cur])
        has[cur] = 1
    memo[b[i]] = 1
print(len(ops))
for i in ops:
    print(*i)
```

