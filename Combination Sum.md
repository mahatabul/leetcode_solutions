# 39. Combination Sum

## Companies

- Apple
- Adobe
- Amazon
- Airbnb
- Facebook
- LinkedIn
- Microsoft
- Bloomberg
- ByteDance

## Difficulty

**Medium**

---

## Problem Statement

Given an array of distinct integers `candidates` and a target integer `target`, return a list of all unique combinations of `candidates` where the chosen numbers sum to `target`. You may return the combinations in any order.

The same number may be chosen from `candidates` an unlimited number of times. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to `target` is less than 150 combinations for the given input.

---

### Example 1:

**Input:**  
`candidates = [2,3,6,7]`, `target = 7`  
**Output:**  
`[[2,2,3],[7]]`  
**Explanation:**

- 2 and 3 are candidates, and `2 + 2 + 3 = 7`. Note that 2 can be used multiple times.
- 7 is a candidate, and `7 = 7`.
- These are the only two combinations.

---

### Example 2:

**Input:**  
`candidates = [2,3,5]`, `target = 8`  
**Output:**  
`[[2,2,2,2],[2,3,3],[3,5]]`

---

### Example 3:

**Input:**  
`candidates = [2]`, `target = 1`  
**Output:**  
`[]`

---

### Constraints:

- `1 <= candidates.length <= 30`
- `2 <= candidates[i] <= 40`
- All elements of `candidates` are distinct.
- `1 <= target <= 40`

---

## Approach

The problem can be solved using **Backtracking**. We explore all possible combinations recursively while ensuring that we do not exceed the `target` value.

### Key Steps:

1. **Recursive Backtracking:**
   - Try adding each candidate to the current combination.
   - If the sum exceeds `target`, backtrack.
   - If the sum matches `target`, store the combination.
   - Continue exploring other possibilities.
2. **Avoid Duplicates:**
   - Since numbers can be reused, the recursion does not move to the next index.
3. **Base Case:**
   - If `target == 0`, store the current combination.
   - If `index == len(candidates)`, stop recursion.

### Complexity Analysis:

- **Time Complexity:** `O(2^T)`, where `T` is the target value.
- **Space Complexity:** `O(T)`, considering recursion depth.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    void s(int index, vector<int> candidate, int target,
           vector<vector<int>> &ans, vector<int> temp) {

        if (index == candidate.size()) {
            if (target == 0) {
                ans.push_back(temp);
            }
            return;
        }

        if (candidate[index] <= target) {
            temp.push_back(candidate[index]);
            s(index, candidate, target - candidate[index], ans, temp);
            temp.pop_back();
        }
        s(index + 1, candidate, target, ans, temp);
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> ans;
        vector<int> temp;
        s(0, candidates, target, ans, temp);
        return ans;
    }
};
```

### Python Solution

```py
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        def backtrack(start, target, path):
            if target == 0:
                res.append(path[:])
                return
            for i in range(start, len(candidates)):
                if candidates[i] > target:
                    continue
                path.append(candidates[i])
                backtrack(i, target - candidates[i], path)
                path.pop()

        res = []
        backtrack(0, target, [])
        return res
```
