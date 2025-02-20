# 63. Unique Paths II

## Company
- C2FO  
- PayTM  
- Cisco  
- VMware  
- Zomato  
- Juspay  
- Amazon  
- Google  
- Oracle  
- Expedia  
- Facebook  
- Bloomberg  
- Atlassian  
- Qualtrics  
- Microsoft  
- Athenahealth  
- DE Shaw India  
- Cruise Automation  
- Quinstreet Software  
- Kreeti Technologies  

## Difficulty
**Medium**

---

## Problem Statement

You are given an `m x n` integer array `grid`. There is a robot initially located at the **top-left corner** (`grid[0][0]`). The robot tries to move to the **bottom-right corner** (`grid[m-1][n-1]`). The robot can **only move either down or right** at any point in time.

An **obstacle** and **space** are marked as **1** and **0** respectively in `grid`. A path that the robot takes **cannot include** any square that is an obstacle.

Return the **number of possible unique paths** that the robot can take to reach the **bottom-right corner**.

The test cases are generated so that the answer will be **≤ 2 * 10⁹**.

---

### Example 1:

**Input:**  
`obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]`  
**Output:**  
`2`  
**Explanation:**  
There is **one obstacle** in the middle of the **3x3** grid above.  
There are **two ways** to reach the **bottom-right corner**:  
1. **Right → Right → Down → Down**  
2. **Down → Down → Right → Right**  

---

### Example 2:

**Input:**  
`obstacleGrid = [[0,1],[0,0]]`  
**Output:**  
`1`  

---

### Constraints:
- `m == obstacleGrid.length`  
- `n == obstacleGrid[i].length`  
- `1 <= m, n <= 100`  
- `obstacleGrid[i][j]` is **0** or **1**  

---

## Approach

1. **Recursive Approach with Memoization:**
   - Define a recursive function `solve(i, j, m, n, dp, obstacleGrid)` to explore paths.
   - If the cell contains an **obstacle (`1`)** or is out of bounds, return **0**.
   - If the **destination** (`m-1, n-1`) is reached, return **1**.

2. **Memoization:**
   - Use a **2D `dp` array** to store the number of unique paths from each cell.
   - If the **subproblem** is already **solved**, return the **stored result** to avoid **recomputation**.

3. **Edge Cases:**
   - If **start** or **end** is **blocked**, return **0** immediately.

4. **Time Complexity:**
   - **O(m × n)** due to **memoization**, as each cell is computed **only once**.
   - **Space Complexity:** **O(m × n)** for the **DP array**.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int solve(int i, int j, int m, int n, vector<vector<int>>& dp,
              vector<vector<int>>& og) {
        // Boundary checks and obstacle check
        if (i >= m || j >= n || og[i][j] == 1) {
            return 0;
        }

        // Reached the bottom-right corner
        if (i == m - 1 && j == n - 1) {
            return 1;
        }

        // Return memoized result
        if (dp[i][j] != -1) {
            return dp[i][j];
        }

        // Calculate paths by moving right and down
        return dp[i][j] = solve(i + 1, j, m, n, dp, og) +
                          solve(i, j + 1, m, n, dp, og);
    }

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();

        // If start or end is an obstacle, no path is possible
        if (obstacleGrid[0][0] == 1 || obstacleGrid[m - 1][n - 1] == 1) {
            return 0;
        }

        vector<vector<int>> dp(m, vector<int>(n, -1));
        return solve(0, 0, m, n, dp, obstacleGrid);
    }
};
```
### Python Solution

```py
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        
        # If start or end is an obstacle
        if obstacleGrid[0][0] == 1 or obstacleGrid[m-1][n-1] == 1:
            return 0
        
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = 1
        
        for i in range(m):
            for j in range(n):
                if obstacleGrid[i][j] == 1:
                    dp[i][j] = 0
                else:
                    if i > 0:
                        dp[i][j] += dp[i-1][j]
                    if j > 0:
                        dp[i][j] += dp[i][j-1]
        
        return dp[-1][-1]

```