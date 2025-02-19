# 62. Unique Paths

## Company
- Ola  
- Zoho  
- Uber  
- DTCC  
- Paytm  
- Cisco  
- Apple  
- Adobe  
- BYJUS  
- Google  
- Oracle  
- VMware  
- Amazon  
- Zomato  
- Twilio  
- Walmart  
- CoinDCX  
- Impetus  
- Directi  
- LinkedIn  
- Snapchat  
- Facebook  
- SAP Labs  
- ByteDance  
- Mathworks  
- Qualtrics  
- Microsoft  
- Bloomberg  
- Atlassian  
- Accolite  
- Salesforce  
- BNY Mellon  
- MONEY View  
- CashKaro.com  
- Goldman Sachs  
- ThoughtWorks  
- Rudder Analytics  
- Cashfree Payments  
- Jio Platform Limited  
- Wheelseye Technology  
- Physicswallah  
- SS Supply Chain Solutions Pvt Ltd  

## Difficulty
**Medium**

---

## Problem Statement

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (`grid[0][0]`). It tries to move to the **bottom-right corner** (`grid[m-1][n-1]`). The robot can **only move either down or right** at any point.

Given the two integers `m` and `n`, return **the number of possible unique paths** that the robot can take to reach the bottom-right corner.

The test cases are generated so that the answer will be **≤ 2 * 10⁹**.

---

### Example 1:

**Input:**  
`m = 3, n = 7`  
**Output:**  
`28`  

---

### Example 2:

**Input:**  
`m = 3, n = 2`  
**Output:**  
`3`  
**Explanation:**  
From the top-left corner, there are **3 ways** to reach the bottom-right corner:  
1. Right → Down → Down  
2. Down → Down → Right  
3. Down → Right → Down  

---

### Constraints:
- `1 <= m, n <= 100`

---

## Approach

1. **Dynamic Programming with Memoization (Top-Down Approach):**
   - Define a recursive function `solve(i, j, m, n, freq, dp)` to explore paths.
   - Use **two possible moves**: **Right (`→`)** and **Down (`↓`)**.
   - Maintain a **frequency matrix** (`freq`) to avoid revisiting nodes.
   - Use **memoization (`dp` array)** to store the results of subproblems.

2. **Base Case:**
   - If we reach the **bottom-right corner**, return `1` (valid path found).

3. **Recurrence Relation:**
   - The total unique paths from `(i, j)` is the sum of:
     - Paths from `(i + 1, j)` (moving **down**).
     - Paths from `(i, j + 1)` (moving **right**).

4. **Time Complexity Analysis:**
   - Since we memoize the results, the **time complexity** is **O(m × n)**.
   - The **space complexity** is also **O(m × n)** due to the DP table.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int solve(int i, int j, int m, int n, vector<vector<int>> &freq, vector<vector<int>> &dp) {
        if (i == m - 1 && j == n - 1) {
            return 1;
        }

        if (dp[i][j] != -1) {
            return dp[i][j];
        }

        int ans = 0;
        int di[] = {1, 0};  // Down, Right
        int dj[] = {0, 1};

        for (int idx = 0; idx < 2; idx++) {
            int ni = i + di[idx];
            int nj = j + dj[idx];

            if (ni < m && nj < n && !freq[ni][nj]) {
                freq[ni][nj] = 1;
                ans += solve(ni, nj, m, n, freq, dp);
                freq[ni][nj] = 0;
            }
        }
        return dp[i][j] = ans;
    }

    int uniquePaths(int m, int n) {
        vector<vector<int>> freq(m, vector<int>(n, 0));
        vector<vector<int>> dp(m, vector<int>(n, -1));

        freq[0][0] = 1;
        return solve(0, 0, m, n, freq, dp);
    }
};
```
### Python Solution
```py
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1] * n for _ in range(m)]
        
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        
        return dp[-1][-1]
```