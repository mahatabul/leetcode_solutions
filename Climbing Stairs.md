# 70. Climbing Stairs

## Company
- Uber  
- Adobe  
- Yahoo  
- Amazon  
- Google  
- Expedia  
- Microsoft  
- Bloomberg  
- Goldman Sachs  

## Difficulty
**Easy**

---

## Problem Statement

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

### Example 1:

**Input:**  
`n = 2`  
**Output:**  
`2`  
**Explanation:**  
There are two ways to climb to the top:  
1. `1 step + 1 step`  
2. `2 steps`  

### Example 2:

**Input:**  
`n = 3`  
**Output:**  
`3`  
**Explanation:**  
There are three ways to climb to the top:  
1. `1 step + 1 step + 1 step`  
2. `1 step + 2 steps`  
3. `2 steps + 1 step`  

### Constraints:
- `1 <= n <= 45`

---

## Approach

1. **Dynamic Programming (Fibonacci Sequence):**
   - The problem follows the Fibonacci sequence because each step can be reached from either one or two steps below.
   - Let `dp[i]` represent the number of ways to reach step `i`.
   - Base cases:
     - `dp[1] = 1` (Only one way to reach step 1)
     - `dp[2] = 2` (Two ways: `1+1` or `2`)
   - Transition formula: `dp[i] = dp[i - 1] + dp[i - 2]`
   - Optimized approach using two variables instead of an array for better space complexity.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 2) {
            return n;
        }

        int pre1 = 1, pre2 = 2;

        for (int i = 3; i <= n; i++) {
            int curr = pre1 + pre2;
            pre1 = pre2;
            pre2 = curr;
        }

        return pre2;
    }
};
```

