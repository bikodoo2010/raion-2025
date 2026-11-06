# raion-2025
```  
import sys
from bisect import bisect_left

input = sys.stdin.readline

n, A, B = map(int, input().split())
r = list(map(int, input().split()))

r.sort()


def check(x):
    dp = [False] * (n + 1)
    pref = [0] * (n + 2)

    dp[0] = True
    pref[1] = 1

    for i in range(1, n + 1):
        k = bisect_left(r, r[i - 1] - x)

        lo = max(i - B, k)
        hi = i - A

        if lo <= hi:
            if pref[hi + 1] - pref[lo] > 0:
                dp[i] = True

        pref[i + 1] = pref[i] + dp[i]

    return dp[n]


l = 0
rr = r[-1] - r[0]

while l < rr:
    mid = (l + rr) // 2

    if check(mid):
        rr = mid
    else:
        l = mid + 1

print(l)```
