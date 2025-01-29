# 1248. Count Number of Nice Subarrays

## Companies
- Adobe  
- Amazon  
- Robolox  
- Booking.Com  

## Difficulty
**Medium**

---

## Problem Statement

Given an array of integers `nums` and an integer `k`, a continuous subarray is called **nice** if there are exactly `k` odd numbers in it. Return the number of nice subarrays.

### Examples

**Example 1:**

**Input:**  
`nums = [1,1,2,1,1], k = 3`  
**Output:**  
`2`  
**Explanation:**  
The nice subarrays are `[1,1,2,1]` and `[1,2,1,1]`.

**Example 2:**

**Input:**  
`nums = [2,4,6], k = 1`  
**Output:**  
`0`  
**Explanation:**  
There are no odd numbers in the array.

**Example 3:**

**Input:**  
`nums = [2,2,2,1,2,2,1,2,2,2], k = 2`  
**Output:**  
`16`

### Constraints:
- `1 <= nums.length <= 50000`
- `1 <= nums[i] <= 10^5`
- `1 <= k <= nums.length`

---

## Approach

The problem can be efficiently solved using a prefix sum approach combined with a hash map to track the counts of the number of odd numbers encountered so far. This method is similar to solving subarray sum equals a target value, where here the "sum" represents the count of odd numbers.

### Key Steps:
1. **Prefix Sum Tracking:** Maintain a running count (`sum`) of the number of odd numbers encountered as we iterate through the array.
2. **Hash Map for Counts:** Use a hash map (`presum`) to store the frequency of each prefix sum (count of odds) encountered. Initialize the map with `presum[0] = 1` to handle subarrays starting from the beginning.
3. **Check for Valid Subarrays:** For each element, after updating the current `sum`, check if `sum - goal` exists in the hash map. If it does, it means there are subarrays ending at the current index with exactly `goal` odd numbers. Add the count of `sum - goal` from the map to the answer.
4. **Update Hash Map:** Increment the count of the current `sum` in the hash map to account for future subarrays.

### Time Complexity:
- **O(n)**, where `n` is the length of the array. Each element is processed once, and hash map operations are average O(1).

### Space Complexity:
- **O(n)**, due to the hash map storing up to `n` different prefix sums in the worst case.

---

## Solution Code

### C++ Solution

```cpp
class Solution {
public:
    int numberOfSubarrays(vector<int>& nums, int goal) {
        map<int, int> presum;
        presum[0] = 1;
        int sum = 0, ans = 0;

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] & 1) {
                sum++;
            }

            if (presum.find(sum - goal) != presum.end() && sum >= goal) {
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
from collections import defaultdict

class Solution:
    def numberOfSubarrays(self, nums, goal):
        presum = defaultdict(int)
        presum[0] = 1
        sum_ = 0
        ans = 0

        for num in nums:
            if num % 2 == 1:  # Check if the number is odd
                sum_ += 1

            if sum_ - goal in presum and sum_ >= goal:
                ans += presum[sum_ - goal]

            presum[sum_] += 1

        return ans

```
