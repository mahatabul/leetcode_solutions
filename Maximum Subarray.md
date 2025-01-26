# 53. Maximum Subarray

## Company
- Uber  
- Apple  
- Adobe  
- Cisco  
- PayTM  
- Amazon  
- Google  
- Shopee  
- VMware  
- Oracle  
- Samsung  
- Infosys  
- LinkedIn  
- Facebook  
- JPMorgan  
- Docusign  
- Microsoft  
- Bloomberg  
- ByteDance  
- Salesforce  
- ServiceNow  
- Goldman Sachs  
- Walmart Global Tech  

## Difficulty
**Medium**

---

## Problem Statement

Given an integer array `nums`, find the subarray with the largest sum, and return its sum.

### Example 1:

Input: nums = [-2,1,-3,4,-1,2,1,-5,4] Output: 6 Explanation: The subarray [4,-1,2,1] has the largest sum 6.


### Example 2:

Input: nums = [1] Output: 1 Explanation: The subarray [1] has the largest sum 1.


### Example 3:

Input: nums = [5,4,-1,7,8] Output: 23 Explanation: The subarray [5,4,-1,7,8] has the largest sum 23.


### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

---

## Approach

1. **Kadane's Algorithm**:
   - Start with an initial `sum = 0` and `max_sum = INT_MIN`.
   - Iterate through the array, adding the current element to the running sum (`sum`).
   - Update `max_sum` with the maximum of `max_sum` and `sum`.
   - If `sum` becomes negative, reset it to `0` to exclude it from the subarray.
   
2. **Time Complexity**:
   - The algorithm runs in **O(n)** since we traverse the array once.
   
3. **Space Complexity**:
   - The algorithm uses **O(1)** additional space.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& a) {
        int sum = 0, n = a.size();
        int max_sum = INT_MIN;
        for (int i = 0; i < n; i++) {
            sum += a[i];
            max_sum = max(sum, max_sum);

            if (sum < 0) {
                sum = 0;
            }
        }
        return max_sum;
    }
};
```
### Python Solution

```py
class Solution:
    def maxSubArray(self, nums):
        max_sum = float('-inf')
        current_sum = 0
        
        for num in nums:
            current_sum += num
            max_sum = max(max_sum, current_sum)
            
            if current_sum < 0:
                current_sum = 0
        
        return max_sum
```
