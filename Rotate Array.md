# 189. Rotate Array

## Companies
- TCS  
- Yahoo  
- Amazon  
- Google  
- Facebook  
- Microsoft  
- Salesforce  

## Difficulty
**Medium**

---

## Problem Statement

Given an integer array `nums`, rotate the array to the right by `k` steps, where `k` is non-negative.

### Example 1:

**Input:**  
`nums = [1,2,3,4,5,6,7]`, `k = 3`  
**Output:**  
`[5,6,7,1,2,3,4]`  
**Explanation:**  
Rotate 1 step to the right: `[7,1,2,3,4,5,6]`  
Rotate 2 steps to the right: `[6,7,1,2,3,4,5]`  
Rotate 3 steps to the right: `[5,6,7,1,2,3,4]`

### Example 2:

**Input:**  
`nums = [-1,-100,3,99]`, `k = 2`  
**Output:**  
`[3,99,-1,-100]`  
**Explanation:**  
Rotate 1 step to the right: `[99,-1,-100,3]`  
Rotate 2 steps to the right: `[3,99,-1,-100]`

### Constraints:
- `1 <= nums.length <= 10^5`
- `-2^31 <= nums[i] <= 2^31 - 1`
- `0 <= k <= 10^5`

---

## Approach

The key insight is to recognize that rotating the array by `k` steps to the right is equivalent to moving the last `k` elements to the front. However, if `k` is larger than the array length `n`, it effectively rotates the array `k % n` times. 

### Steps:
1. **Compute Effective Rotation**: Calculate `k % n` to handle cases where `k` is larger than the array length.
2. **Slice and Concatenate**: The rotated array can be formed by concatenating the last `k` elements of the original array with the first `n - k` elements.

### Time Complexity:
- **O(n)**, where `n` is the length of the array. This is because slicing and concatenating arrays takes linear time.

### Space Complexity:
- **O(n)**, as slicing creates new lists. However, modifying the array in-place by using `nums[:]` allows us to maintain the original reference.

---

## Solutions

### Python Solution

```python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        k %= n
        nums[:] = nums[-k:] + nums[:-k]
```

### C++ Solution

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size(), j = 0;
        k = k % n;
        int d = n - k;
        vector<int> temp(n);

        for (int i = d; i < n; i++) {
            temp[j++] = nums[i];
        }
        for (int i = 0; i < d; i++) {
            temp[j++] = nums[i];
        }

        for (int i = 0; i < n; i++) {
            nums[i] = temp[i];
        }       
    }
};
```