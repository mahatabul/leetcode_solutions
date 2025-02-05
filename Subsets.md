# 78. Subsets

## Company

- Uber
- Apple
- Adobe
- Amazon
- Google
- Reddit
- Twitter
- Facebook
- Bloomberg
- Microsoft

## Difficulty

**Medium**

---

## Problem Statement

Given an integer array `nums` of **unique elements**, return **all possible subsets** (the power set).

The solution set **must not contain duplicate subsets**. Return the solution in **any order**.

---

### Example 1:

**Input:**  
`nums = [1, 2, 3]`  
**Output:**  
`[[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]`

---

### Example 2:

**Input:**  
`nums = [0]`  
**Output:**  
`[[], [0]]`

---

### Constraints:

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- All the numbers of `nums` are **unique**.

---

## Approach

### **1. Bit Manipulation (Iterative Method):**

- Each subset can be represented by a binary number:

  - For example, for `nums = [1, 2, 3]`:
    - `000` → `[]` (empty subset)
    - `001` → `[1]`
    - `010` → `[2]`
    - `011` → `[1, 2]`
    - ... and so on.

- Total number of subsets = \(2^n\), where \(n\) is the size of `nums`.

- **Steps:**

  1. Generate numbers from `0` to \(2^n - 1\).
  2. For each number, check its bits.
  3. If the `j-th` bit is set, include `nums[j]` in the current subset.

- **Complexity:**
  - **Time Complexity:** \(O(n \cdot 2^n)\)
  - **Space Complexity:** \(O(2^n)\) (for the output)

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans;
        int n = nums.size();
        int limit = 1 << n; // Total number of subsets = 2^n

        for (int i = 0; i < limit; i++) {
            vector<int> subset;
            for (int j = 0; j < n; j++) {
                if (i & (1 << j)) { // Check if the j-th bit is set
                    subset.push_back(nums[j]);
                }
            }
            ans.push_back(subset);
        }
        return ans;
    }
};
```

### Python Solution

```py
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        result = []

        for i in range(1 << n):  # Loop from 0 to 2^n - 1
            subset = []
            for j in range(n):
                if i & (1 << j):  # Check if the j-th bit is set
                    subset.append(nums[j])
            result.append(subset)

        return result
```
