# Description

Given an integer `n`, return the least number of perfect square numbers that sum to `n`.

A <b>perfect square</b> is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, `1`, `4`, `9`, and `16` are perfect squares while `3` and `11` are not.

<b>Example 1:</b>

```bash
Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
```

<b>Example 2:</b>

```bash
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

<b>Constraints:</b>

`1 <= n <= 104`

# Approach
1. If `n` in `memo`, then return `n`
2. If `n` is 0, then base case is reached
3. initialize `positive infinity float` variable to store the minimum number of perfect squares needed for the current value of `n`. 
4. iterates  all possible perfect squares less than or equal to n, from `1` to the square root of `n`.
5. calculates the minimum number of perfect squares needed for the remaining value `(n - i * i)` recursively and adds `1` (to include the current perfect square `i * i`). Then, updates `min_sq` with the minimum of its current value and the calculated value.
6. memoizes the result for the current `n` by storing `min_sq` in the memoization dictionary.

# Complexity 
- TC: $O(n*\sqrt{n}), Θ(n*\sqrt{n}), Ω(n*\sqrt{n})$
- SC: $O(n)$

# Code

```python3
import math

class Solution:
    dp = [0] # declare dp class variable

    def numSquares(self, n: int) -> int:
        dp = self.dp
        perfectSq = [pow(i,2) for i in range(1, int(sqrt(n))+1)] # precompute the perfect squares.
        
        while len(dp) < n+1: # build dp < length n+1
            dpI = math.inf # store the min number of perfect squares needed for the current number being processed
            for ps in perfectSq: # dp equation
                if len(dp) < ps: break # base case
                dpI = min(dpI, 1 + dp[n-ps])
            dp.append(dpI)
        return dp[n]
```

# Result
<img width="683" alt="image" src="https://github.com/nicholasw2022/nicholasw2022/assets/143755743/256ece62-71b4-43ab-b8d8-1f53dc44b259">

