# 931. Minimum Falling Path Sum

## Company
- Google  

## Difficulty
**Medium**

---

## Problem Statement

Given an **n x n** array of integers **matrix**, return the **minimum sum** of **any falling path** through the **matrix**.

A **falling path** starts at **any element** in the **first row** and **chooses** the **element** in the **next row** that is either:  
- **Directly below** `(row + 1, col)`  
- **Diagonally left** `(row + 1, col - 1)`  
- **Diagonally right** `(row + 1, col + 1)`

---

### Example 1:

**Input:**  
`matrix = [[2,1,3],[6,5,4],[7,8,9]]`

**Output:**  
`13`

**Explanation:**  
There are **two falling paths** with a **minimum sum** as shown:  

2 1 3 6 5 4 7 8 9


The **minimum falling path sum** is `1 + 4 + 8 = 13`.  

---

### Example 2:

**Input:**  
`matrix = [[-19,57],[-40,-5]]`

**Output:**  
`-59`

**Explanation:**  
The **falling path** with the **minimum sum** is `-19 + -40 = -59`.

---

### Constraints:
- `n == matrix.length == matrix[i].length`
- `1 <= n <= 100`
- `-100 <= matrix[i][j] <= 100`

---

## Approach

### Dynamic Programming (DP) with Space Optimization

1. **Initialize:**  
   Create **two 1D arrays** `pre` and `curr` of **size `n`**:  
   - `pre`: Stores the **minimum path sum** of the **previous row**.  
   - `curr`: Computes the **current row's minimum path sums**.

2. **Base Case:**  
   Copy the **first row** of `matrix` to `pre` as **starting points** for **falling paths**.

3. **Iterate Through Rows:**  
   For **each row**, compute the **minimum path sum** for **each column** using:  
   - **Directly below** (`path3 = pre[col]`).  
   - **Diagonally left** (`path1 = pre[col - 1]` if **valid**).  
   - **Diagonally right** (`path2 = pre[col + 1]` if **valid**).  

4. **Update `pre`:**  
   Once a **row is completed**, **copy `curr` into `pre`** to **prepare** for the **next row**.

5. **Return Result:**  
   The **minimum value** in the **last `pre` array** gives the **minimum falling path sum**.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int minFallingPathSum(vector<vector<int>>& matrix) {

        int n = matrix.size();

        vector<int> pre(n, -101);
        vector<int> curr(n, -101);

        // Initialize pre with the first row of the matrix
        for (int i = 0; i < n; i++) {
            pre[i] = matrix[0][i];
        }

        // Traverse the matrix starting from the second row
        for (int row = 1; row < n; row++) {
            for (int col = 0; col < n; col++) {
                
                int path1 = INT_MAX, path2 = INT_MAX, path3 = INT_MAX;

                // Diagonally left
                if (col - 1 >= 0)
                    path1 = pre[col - 1];

                // Diagonally right
                if (col + 1 < n) 
                    path2 = pre[col + 1];

                // Directly below
                path3 = pre[col];

                // Calculate the current minimum path sum
                curr[col] = matrix[row][col] + min({path1, path2, path3});
            }

            // Update pre to the current row results
            pre = curr;
        }

        // Return the minimum value from the last row
        return *min_element(pre.begin(), pre.end());
    }
};
```

### Python Solution

class Solution:
    def minFallingPathSum(self, matrix: List[List[int]]) -> int:
        n = len(matrix)

        # Iterate from the second last row to the top
        for row in range(n - 2, -1, -1):
            for col in range(n):
                # Get minimum of the three possible downward paths
                min_below = matrix[row + 1][col]
                
                if col > 0:
                    min_below = min(min_below, matrix[row + 1][col - 1])
                
                if col < n - 1:
                    min_below = min(min_below, matrix[row + 1][col + 1])
                
                matrix[row][col] += min_below

        # The answer will be the minimum value in the first row
        return min(matrix[0])
```