# 992. Subarrays with K Different Integers

## Company
- Uber  
- Adobe  
- Apple  
- TikTok  
- Oracle  
- Amazon  
- Google  
- Airbnb  
- Expedia  
- DE Shaw  
- Facebook  

## Difficulty
**Hard**

---

## Problem Statement

Given an integer array `nums` and an integer `k`, return the number of good subarrays of `nums`.

A good array is an array where the number of different integers in that array is exactly `k`.

A subarray is a contiguous part of an array.

### Example 1:

Input: nums = [1,2,1,2,3], k = 2 Output: 7 Explanation: Subarrays formed with exactly 2 different integers: [1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2]


### Example 2:

Input: nums = [1,2,1,3,4], k = 3 Output: 3 Explanation: Subarrays formed with exactly 3 different integers: [1,2,1,3], [2,1,3], [1,3,4].


### Constraints:
- `1 <= nums.length <= 2 * 10^4`
- `1 <= nums[i], k <= nums.length`

---

## Approach

1. **Helper Function**:
   - Implement a helper function `solve()` to calculate the number of subarrays with at most `k` different integers.
   - Use a sliding window approach with a hash map to track the frequency of integers in the current window.

2. **Calculate Result**:
   - The number of subarrays with exactly `k` different integers is the difference between subarrays with at most `k` and subarrays with at most `k - 1`.

3. **Time Complexity**:
   - The algorithm runs in **O(n)**, where `n` is the size of the array, as each element is processed at most twice (once for addition and once for removal).

4. **Space Complexity**:
   - The space complexity is **O(k)**, due to the hash map storing at most `k` keys.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int solve(vector<int>& s, int k) {
        int l = 0, maxlen = 0;
        map<int, int> hmap;

        for (int r = 0; r < s.size(); r++) {
            hmap[s[r]]++;

            while (hmap.size() > k) {
                hmap[s[l]]--;
                if (hmap[s[l]] == 0) {
                    hmap.erase(s[l]);
                }
                l++;
            }

            maxlen += r - l + 1;
        }
        return maxlen;
    }

    int subarraysWithKDistinct(vector<int>& s, int k) {
        return solve(s, k) - solve(s, k - 1);
    }
};
```

### Python Solution

```py
class Solution:
    def solve(self, nums, k):
        l = 0
        maxlen = 0
        hmap = {}

        for r in range(len(nums)):
            hmap[nums[r]] = hmap.get(nums[r], 0) + 1

            while len(hmap) > k:
                hmap[nums[l]] -= 1
                if hmap[nums[l]] == 0:
                    del hmap[nums[l]]
                l += 1

            maxlen += r - l + 1

        return maxlen

    def subarraysWithKDistinct(self, nums, k):
        return self.solve(nums, k) - self.solve(nums, k - 1)
```        