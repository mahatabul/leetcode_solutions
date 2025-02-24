# 120. Triangle

## Company
- Amazon  
- Microsoft  

## Difficulty
**Medium**

---

## Problem Statement

Given a **triangle array**, return the **minimum path sum** from **top** to **bottom**.

For each step, you may **move** to an **adjacent number** of the row below.  

More formally, if you are on **index `i`** on the **current row**, you may **move** to either **index `i`** or **index `i + 1`** on the **next row**.

---

### Example 1:

**Input:**  
`triangle = [[2],[3,4],[6,5,7],[4,1,8,3]]`  

**Output:**  
`11`  

**Explanation:**  
The triangle looks like:  
<pre>
   2 <br>
  3 4 <br>
 6 5 7 <br>
4 1 8 3 <br>
</pre>



The **minimum path sum** from **top** to **bottom** is:  
`2 + 3 + 5 + 1 = 11`  

---

### Example 2:

**Input:**  
`triangle = [[-10]]`  

**Output:**  
`-10`  

---

### Constraints:
- `1 <= triangle.length <= 200`  
- `triangle[0].length == 1`  
- `triangle[i].length == triangle[i - 1].length + 1`  
- `-10^4 <= triangle[i][j] <= 10^4`  

---

### Follow Up:
- Can you solve this using **only** `O(n)` **extra space**, where `n` is the **total number of rows** in the **triangle**?

---

## Approach

### Recursive Approach with Memoization

1. **Recursive Function:**  
   Define a **recursive function** `minimumTotalsolve(row, col, triangle, dp)` to calculate the **minimum path sum** starting from `(row, col)` to the **bottom** of the **triangle**.

2. **Base Case:**  
   When the **last row** is reached, return the **value** of the **current cell**.

3. **Memoization:**  
   If the **subproblem** is **already solved**, return the **stored result** in `dp[row][col]`.

4. **Recursive Calls:**  
   - **Down Move:** From `(row, col)` to `(row + 1, col)`.  
   - **Down-Right Move:** From `(row, col)` to `(row + 1, col + 1)`.  

5. **Update DP Array:**  
   `dp[row][col] = triangle[row][col] + min(down, dright)`  

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int minimumTotalsolve(int row, int col, vector<vector<int>>& tri,
                          vector<vector<int>>& dp) {
        // Base case: If we are at the last row
        if (row == tri.size() - 1) {
            return tri[row][col];
        }

        // Return the cached result if available
        if (dp[row][col] != -1) {
            return dp[row][col];
        }

        // Recursive calls for downward and down-right moves
        int down = minimumTotalsolve(row + 1, col, tri, dp);
        int dright = minimumTotalsolve(row + 1, col + 1, tri, dp);

        // Store the computed result in dp array
        return dp[row][col] = tri[row][col] + min(down, dright);
    }

    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();

        // DP array for memoization
        vector<vector<int>> dp(n, vector<int>(n, -1));

        // Start solving from the top of the triangle
        return minimumTotalsolve(0, 0, triangle, dp);
    }
};
```

### Python Solution
```py
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        n = len(triangle)
        
        # Start with the last row of the triangle as the initial 'dp' array
        dp = triangle[-1]
        
        # Bottom-up approach
        for row in range(n - 2, -1, -1):
            for col in range(len(triangle[row])):
                dp[col] = triangle[row][col] + min(dp[col], dp[col + 1])
        
        # The top of the triangle now holds the minimum path sum
        return dp[0]
```
