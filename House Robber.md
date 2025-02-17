# 198. House Robber

## Company
- Apple  
- Cisco  
- Adobe  
- Amazon  
- Google  
- Facebook  
- Microsoft  
- Bloomberg  
- Walmart Global Tech  

## Difficulty
**Medium**

---

## Problem Statement

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. The only constraint stopping you from robbing each of them is that adjacent houses have security systems connected, and it will automatically contact the police if two adjacent houses are broken into on the same night.

Given an integer array `nums` representing the amount of money in each house, return the **maximum amount of money** you can rob tonight without alerting the police.

---

### Example 1:

**Input:**  
`nums = [1,2,3,1]`  
**Output:**  
`4`  
**Explanation:**  
Rob house 1 (money = `1`) and then rob house 3 (money = `3`).  
Total amount you can rob = `1 + 3 = 4`.

---

### Example 2:

**Input:**  
`nums = [2,7,9,3,1]`  
**Output:**  
`12`  
**Explanation:**  
Rob house 1 (money = `2`), rob house 3 (money = `9`), and rob house 5 (money = `1`).  
Total amount you can rob = `2 + 9 + 1 = 12`.

---

### Constraints:
- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 400`

---

## Approach

1. **Dynamic Programming:**
   - Use an array `dp[i]` where `dp[i]` represents the maximum money that can be robbed from the first `i` houses.
   - Base cases:
     - `dp[0] = nums[0]`
     - `dp[1] = max(nums[0], nums[1])`
   - Transition formula:  
     - `dp[i] = max(dp[i - 1], nums[i] + dp[i - 2])`
   - Instead of using an array, optimize space by keeping track of only the last two values (`pre1` and `pre2`).

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.empty()) return 0;
        if (nums.size() == 1) return nums[0];

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
};
```

### Python Solution

```py
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        if len(nums) == 1:
            return nums[0]

        pre2, pre1 = 0, nums[0]

        for i in range(1, len(nums)):
            take = nums[i] + (pre2 if i > 1 else 0)
            not_take = pre1

            curr = max(take, not_take)

            pre2, pre1 = pre1, curr

        return pre1
```