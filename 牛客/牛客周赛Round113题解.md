# A 小红取模

显然  $x \mod 9$ 即为答案。

```py
print(int(input())%9)
```

硬算可以（

```py
print(sum(map(int, list(input())))%9)
```



# B.小红的复数

按题意模拟即可

```py
MOD = 10**9 + 7
n = int(input())

x = 1
y = 0
for _ in range(n):
    xx, yy = map(int, input().split())
    tx = (x*xx - y*yy+MOD)%MOD
    ty = (x*yy+y*xx)%MOD
    x = tx
    y = ty
print(x, y)
```



# c.小红的k次方

由于 $30 = 2 \times 3 \times 5$，统计数组中有几个 $2, 3, 5$ 取最小即可。

```py
n = int(input())
c2 = c3 = c5 = 0
a = list(map(int, input().split()))

for i in a:
    while i%2 == 0:
        c2 += 1
        i//=2
    while i%3==0:
        c3 += 1
        i//=3
    while i%5==0:
        c5 += 1
        i//=5

print(min(c2, c3, c5))
```



# D.小红模5

易得新整数对 $5$ 取模的值只跟结尾有关，每个结尾会出现 $(n-1)!$ 次。

所以答案为$(\sum \limits_{i=1}^{n} i \mod 5) * (n-1)!)$

```cpp
n = int(input())
MOD = 10**9+7
fac = [0 for i in range(n+1)]
fac[0] = 1
for i in range(1, n+1):
    fac[i] = (fac[i-1] * i)%MOD

t = 0
for i in range(1, n+1):
    t = (t + i%5)%MOD

print(t*fac[n-1]%MOD)
```



# E.二小姐取数

定义 $dp[i][j]$ 为从 数组中取 $i$ 个数字，和对 $495$ 取模后的结果为 $j$ 的方案数。

则可以枚举每个数 $a_i$，对 $j \in [0, i-1] , k \in [0, 494]$ 有 $dp[j+1][(k+a_i)\%495] += dp[j][k]$ 

由于 $b$ 的元素数量不超过 $a$ 的，我们可以对 $dpb$ 求前缀和，再数组卷积即可求出答案。

```py
MOD = 10**9+7

n = int(input())
a = [0] + list(map(int, input().split()))
b = [0] + list(map(int, input().split()))

dpa = [[0 for i in range(495)] for i in range(n+1)]
dpb = [[0 for i in range(495)] for i in range(n+1)]
dpa[0][0] = 1
dpb[0][0] = 1
for i in range(1, n+1):
    for j in range(i-1, -1, -1):
        for k in range(495):
            dpa[(j+1)][(k+a[i])%495] = (dpa[(j+1)][(k+a[i])%495] + dpa[j][k])%MOD
            dpb[(j+1)][(k+b[i])%495] = (dpb[(j+1)][(k+b[i])%495] + dpb[j][k])%MOD
           
preb = [[0 for i in range(495)] for i in range(n+1)]
preb[0][0] = 1
for i in range(1, n+1):
    for j in range(495):
        preb[i][j] = (preb[i-1][j] + dpb[i][j])%MOD
        
cnt = [0 for i in range(495)]
for i in range(n+1):
    x  = dpa[i]
    y = preb[i]
    for j in range(495):
        for k in range(495):
            cnt[(j+k)%495] = (cnt[(j+k)%495] + x[j] * y[k]%MOD)%MOD
print(*cnt)
```



# F.二小姐的区间查询

由于 $495 = 3 * 3 * 5 * 11$，对每个数，我们区分数是否有$>=2/=1/=0$个 $3$，$>1/=0$ 个 $5$ ，$>1/=0$ 个 $11$  共 $12$ 种状态。

对每种状态，开一个树状数组去维护 $[l, r]$ 内有几种。

每次查询，两两匹配每种数字，统计答案即可。

```py
class BIT:
    def __init__(self, n):
        self.n = n
        self.c = [0 for i in range(n+1)]
    
    def add(self, x, d):
        while x <= self.n:
            self.c[x] += d
            x += x&-x
    
    def  query(self, x):
        if x <= 0:
            return 0
        res = 0
        while x:
            res += self.c[x]
            x -= x&-x
        return res
    
    def range(self, l, r):
        return self.query(r) - self.query(l-1)
    
memo = {}
memo2 = {}
idx = 0
for i in range(0, 3):
    for j in range(0, 2):
        for k in range(0, 2):
            memo[i*100+j*10+k] = idx
            memo2[idx] = i*100+j*10+k
            idx += 1

def cal(x):
    c3 = c5 = c11 = 0
    while x%3 == 0:
        c3 += 1
        x //= 3
    while x%5 == 0:
        c5 += 1
        x //= 5
    while x % 11 == 0:
        c11 += 1
        x //= 11
    c3 = min(2, c3)
    c5 = min(1, c5)
    c11 = min(1, c11)
    return memo[c3 *100 + c5*10 + c11]
    
def check(x, y):
    a1 = x//100
    b1 = x//10%10
    c1 = x%10
    a2 = y//100
    b2 = y//10%10
    c2 = y%10
    return a1 + a2 >= 2 and b1 + b2 >= 1 and c1 + c2 >= 1
    
n, q = map(int, input().split())
a = [0] + list(map(int, input().split()))

b = [BIT(n) for i in range(12)]

for i in range(1, n+1):
    b[cal(a[i])].add(i, 1)

for _ in range(q):
    op, x, y = map(int, input().split())
    if  op == 1:
        b[cal(a[x])].add(x, -1)
        a[x] = y
        b[cal(a[x])].add(x, 1)
    else:
        ans = 0
        cnt = [b[i].range(x, y) for i in range(12)]
        for i in range(12):
            for j in range(i+1, 12):
                if check(memo2[i], memo2[j]):
                    ans += cnt[i] * cnt[j]
            if check(memo2[i], memo2[i]):
                ans += cnt[i] * (cnt[i]-1)//2
        print(ans)
```

