# 930. Binary Subarrays With Sum

## Company
- Uber  
- Apple  
- Amazon  
- Google  
- C3 IoT  

## Difficulty
**Medium**

---

## Problem Statement

Given a binary array `nums` and an integer `goal`, return the number of non-empty subarrays with a sum equal to the `goal`.

A subarray is a contiguous part of the array.

### Example 1:

Input: nums = [1,0,1,0,1], goal = 2 Output: 4 Explanation: The 4 subarrays are bolded and underlined below: [1,0,1,0,1] [1,0,1,0,1] [1,0,1,0,1] [1,0,1,0,1]


### Example 2:

Input: nums = [0,0,0,0,0], goal = 0 Output: 15


### Constraints:
- `1 <= nums.length <= 3 * 10^4`
- `nums[i]` is either 0 or 1.
- `0 <= goal <= nums.length`

---

## Approach

1. **Prefix Sum and Hash Map**:
   - Maintain a running sum (`sum`) of the elements while iterating through the array.
   - Use a hash map (`presum`) to store the frequency of each prefix sum encountered so far.
   - For each new sum, check if `sum - goal` exists in the hash map. If it does, it means there is a subarray that sums up to the goal.
   
2. **Time Complexity**:
   - The algorithm runs in **O(n)** because we iterate through the array once and perform constant-time operations for each element.
   
3. **Space Complexity**:
   - The space complexity is **O(n)** because we use a hash map to store prefix sums.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int numSubarraysWithSum(vector<int>& nums, int goal) {
        map<int, int> presum;
        presum[0] = 1;
        int sum = 0, ans = 0;

        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            if (presum.find(sum - goal) != presum.end()) {
                ans += presum[sum - goal];
            }

            presum[sum]++;
        }

        return ans;
    }
};

```

### Python Solution

```py

class Solution:
    def numSubarraysWithSum(self, nums, goal):
        presum = {0: 1}
        sum = 0
        ans = 0
        
        for num in nums:
            sum += num
            if sum - goal in presum:
                ans += presum[sum - goal]
            presum[sum] = presum.get(sum, 0) + 1
            
        return ans

```        