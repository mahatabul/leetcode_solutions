# 1004. Max Consecutive Ones III

## Company
- Apple  
- Google  
- Amazon  
- Facebook  
- Microsoft  
- ByteDance  
- Bloomberg  

## Difficulty
**Medium**

---

## Problem Statement

Given a binary array `nums` and an integer `k`, return the maximum number of consecutive `1`s in the array if you can flip at most `k` `0`s.

### Example 1:

Input: nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2 Output: 6 Explanation: [1,1,1,0,0,1,1,1,1,1,1] Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.


### Example 2:

Input: nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], k = 3 Output: 10 Explanation: [0,0,1,1,1,1,1,1,1,1,1,1,0,0,0,1,1,1,1] Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.


### Constraints:
- `1 <= nums.length <= 10^5`
- `nums[i]` is either `0` or `1`.
- `0 <= k <= nums.length`

---

## Approach

1. **Sliding Window Technique**:
   - Use a two-pointer approach to maintain a sliding window.
   - Count the number of zeros in the current window using a variable (`ktemp`).
   - If the number of zeros exceeds `k`, move the left pointer to shrink the window until the condition is satisfied.

2. **Time Complexity**:
   - The algorithm runs in **O(n)** since each element is processed at most twice (once by the right pointer and once by the left pointer).

3. **Space Complexity**:
   - The space complexity is **O(1)** because only a fixed number of variables are used.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int ans = 0;
        int l = 0;
        int ktemp = 0;

        for (int r = 0; r < nums.size(); r++) {
            if (nums[r] == 0) {
                ktemp++;
            }

            while (ktemp > k) {
                if (nums[l] == 0) {
                    ktemp--;
                }
                l++;
            }

            ans = max(ans, r - l + 1);
        }
        return ans;
    }
};
```
### Python Solution
```py
class Solution:
    def longestOnes(self, nums, k):
        ans = 0
        l = 0
        ktemp = 0

        for r in range(len(nums)):
            if nums[r] == 0:
                ktemp += 1

            while ktemp > k:
                if nums[l] == 0:
                    ktemp -= 1
                l += 1

            ans = max(ans, r - l + 1)
        
        return ans
        
```