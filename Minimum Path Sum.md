# 64. Minimum Path Sum

## Company
- Uber  
- Apple  
- GEICO  
- Amazon  
- Google  
- Oracle  
- Square  
- Microsoft  
- Goldman Sachs  

## Difficulty
**Medium**

---

## Problem Statement

Given an `m x n` grid filled with **non-negative** numbers, find a **path** from the **top-left** to the **bottom-right**, which **minimizes** the **sum** of all numbers along its path.

You can only move **either down** or **right** at any point in time.

---

### Example 1:

**Input:**  
`grid = [[1,3,1],[1,5,1],[4,2,1]]`  
**Output:**  
`7`  
**Explanation:**  
The **minimum path** with the **smallest sum** is:  
`1 → 3 → 1 → 1 → 1 = 7`

---

### Example 2:

**Input:**  
`grid = [[1,2,3],[4,5,6]]`  
**Output:**  
`12`  
**Explanation:**  
The **minimum path** with the **smallest sum** is:  
`1 → 2 → 3 → 6 = 12`

---

### Constraints:
- `m == grid.length`  
- `n == grid[i].length`  
- `1 <= m, n <= 200`  
- `0 <= grid[i][j] <= 200`  

---

## Approach

### Recursive Approach with Memoization

1. **Recursive Function:**  
   Define a recursive function `solve(i, j, grid, dp)` to calculate the **minimum path sum** from cell `(i, j)` to the **bottom-right corner**.

2. **Base Case:**  
   If `(i, j)` is the **bottom-right corner**, return `grid[i][j]`.

3. **Memoization:**  
   If the **subproblem** is **already solved**, return the **stored result** in `dp[i][j]`.

4. **Recursive Calls:**  
   - Move **down** `(i + 1, j)` if **within bounds**.  
   - Move **right** `(i, j + 1)` if **within bounds**.  

5. **Update DP Array:**  
   `dp[i][j] = grid[i][j] + min(down, right)`  

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int solve(int i, int j, vector<vector<int>>& grid, vector<vector<int>>& dp) {
        int m = grid.size();
        int n = grid[0].size();

        // Base case: Reached the bottom-right corner
        if (i == m - 1 && j == n - 1) {
            return grid[i][j];
        }

        // If already computed, return the stored value
        if (dp[i][j] != -1) {
            return dp[i][j];
        }

        int down = INT_MAX, right = INT_MAX;

        // Recursive calls to move down and right
        if (i + 1 < m) {
            down = solve(i + 1, j, grid, dp);
        }
        if (j + 1 < n) {
            right = solve(i, j + 1, grid, dp);
        }

        // Store the result in dp array
        return dp[i][j] = grid[i][j] + min(down, right);
    }

    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();

        // Initialize dp array with -1 for memoization
        vector<vector<int>> dp(m, vector<int>(n, -1));

        return solve(0, 0, grid, dp);
    }
};
```

### Python Solution

```py
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        
        # DP array to store minimum path sums
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = grid[0][0]

        # Fill the first row
        for j in range(1, n):
            dp[0][j] = dp[0][j-1] + grid[0][j]

        # Fill the first column
        for i in range(1, m):
            dp[i][0] = dp[i-1][0] + grid[i][0]

        # Fill the rest of the dp array
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])

        # The bottom-right corner contains the minimum path sum
        return dp[-1][-1]
```