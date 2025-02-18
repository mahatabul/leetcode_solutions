# 213. House Robber II

## Company
- Google  
- Amazon  

## Difficulty
**Medium**

---

## Problem Statement

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. However, all houses are arranged in a **circle**, meaning the first house is adjacent to the last one. 

Meanwhile, adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses are broken into on the same night.

Given an integer array `nums` representing the amount of money in each house, return the **maximum amount of money** you can rob tonight without alerting the police.

---

### Example 1:

**Input:**  
`nums = [2,3,2]`  
**Output:**  
`3`  
**Explanation:**  
You cannot rob house `1` (money = `2`) and then rob house `3` (money = `2`), because they are adjacent houses.

---

### Example 2:

**Input:**  
`nums = [1,2,3,1]`  
**Output:**  
`4`  
**Explanation:**  
Rob house `1` (money = `1`) and then rob house `3` (money = `3`).  
Total amount you can rob = `1 + 3 = 4`.

---

### Example 3:

**Input:**  
`nums = [1,2,3]`  
**Output:**  
`3`

---

### Constraints:
- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`

---

## Approach

1. **Dynamic Programming with Two Cases:**
   - Since houses are arranged in a circle, **we cannot rob both the first and last house**.
   - We solve this problem using **two separate cases**:
     - **Case 1:** Rob houses from index `0` to `n-2` (excluding the last house).
     - **Case 2:** Rob houses from index `1` to `n-1` (excluding the first house).
   - Compute the maximum of both cases to get the final answer.
   - Use the **House Robber I** approach (`rob1` function) to solve each case.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int rob1(vector<int>& nums) {
        int pre2 = 0;
        int pre1 = nums[0];
        int take = 0, not_take = 0;

        for (int i = 1; i < nums.size(); i++) {
            take = nums[i];
            if (i > 1) {
                take += pre2;
            }
            not_take = pre1;

            int curr = max(take, not_take);
            pre2 = pre1;
            pre1 = curr;
        }

        return pre1;
    }

    int rob(vector<int>& nums) {
        if (nums.size() == 1) {
            return nums[0];
        }

        vector<int> temp1(nums.begin() + 1, nums.end());
        vector<int> temp2(nums.begin(), nums.end() - 1);

        return max(rob1(temp1), rob1(temp2));
    }
};
```

### Python Solution

```py
class Solution:
    def rob1(self, nums: List[int]) -> int:
        pre2, pre1 = 0, nums[0]

        for i in range(1, len(nums)):
            take = nums[i] + (pre2 if i > 1 else 0)
            not_take = pre1

            curr = max(take, not_take)
            pre2, pre1 = pre1, curr

        return pre1

    def rob(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return nums[0]

        return max(self.rob1(nums[1:]), self.rob1(nums[:-1]))
```