# 217. Contains Duplicate

## Company
- TCS  
- Uber  
- Adobe  
- Apple  
- Yahoo  
- Amazon  
- Google  
- Microsoft  
- Bloomberg  

## Difficulty
**Easy**

---

## Problem Statement

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is **distinct**.

---

### Example 1:

**Input:**  
`nums = [1, 2, 3, 1]`  
**Output:**  
`true`  
**Explanation:**  
The element `1` occurs at the indices `0` and `3`.

---

### Example 2:

**Input:**  
`nums = [1, 2, 3, 4]`  
**Output:**  
`false`  
**Explanation:**  
All elements are distinct.

---

### Example 3:

**Input:**  
`nums = [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]`  
**Output:**  
`true`  
**Explanation:**  
Multiple elements occur more than once (`1`, `3`, `4`, `2`).

---

### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

---

## Approach

1. **Using a Hash Map (Frequency Counter):**
   - Iterate through the array and store the frequency of each element in a hash map.
   - If an element’s frequency becomes `2` or more, return `true` immediately.
   - If the loop completes without finding any duplicates, return `false`.

2. **Optimizations:**
   - Time Complexity: **O(n)** (where `n` is the size of the array).
   - Space Complexity: **O(n)** (for the hash map).

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        map<int, int> hmap;

        for (int i = 0; i < nums.size(); i++) {
            hmap[nums[i]]++; // Increment the count of the current number
            if (hmap[nums[i]] >= 2) {
                return true; // Duplicate found
            }
        }
        return false; // No duplicates found
    }
};
```

### Python Solution
```py
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        seen = set()

        for num in nums:
            if num in seen:
                return True  # Duplicate found
            seen.add(num)

        return False  # No duplicates found

```        
