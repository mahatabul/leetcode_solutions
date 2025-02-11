# 46. Permutations

## Company
- SAP  
- TCS  
- Oyo  
- eBay  
- Uber  
- DTCC  
- Yahoo  
- PayTM  
- Cvent  
- Dunzo  
- Apple  
- Adobe  
- Amazon  
- Garena  
- Oracle  
- VMware  
- Google  
- GoDaddy  
- Infosys  
- BirdEye  
- Facebook  
- Flipkart  
- Accolite  
- LinkedIn  
- Barclays  
- Atlassian  
- ByteDance  
- Accenture  
- Indiamart  
- Cognizant  
- Microsoft  
- Bloomberg  
- Salesforce  
- Gray Orange  
- Walmart Labs  
- Hyundai Mobis  
- Thought Works  
- Goldman Sachs  
- Coalition Tech  
- Publicis Sapient  

## Difficulty
**Medium**

---

## Problem Statement

Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in any order.

---

### Example 1:

**Input:**  
`nums = [1, 2, 3]`  
**Output:**  
`[[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]]`

---

### Example 2:

**Input:**  
`nums = [0, 1]`  
**Output:**  
`[[0, 1], [1, 0]]`

---

### Example 3:

**Input:**  
`nums = [1]`  
**Output:**  
`[[1]]`

---

### Constraints:
- `1 <= nums.length <= 6`
- `-10 <= nums[i] <= 10`
- All the integers of `nums` are unique.

---

## Approach

1. **Backtracking Approach:**
   - We use a backtracking technique where we attempt to build all possible permutations by exploring each number in the `nums` array.
   - We maintain a frequency array to mark which elements have been used.
   - For each element, we try to add it to the current permutation and recursively generate the next element until the entire permutation is formed.
   - Once a permutation is complete, we store it in the answer array.

2. **Optimizations:**
   - Time Complexity: **O(n!)** (where `n` is the length of the array).
   - Space Complexity: **O(n)** (for the recursion stack and frequency array).

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    void permutations(vector<int>& nums, vector<int>& temp,
                      vector<vector<int>>& ans, vector<int> freq) {
        if (temp.size() == nums.size()) {
            ans.push_back(temp);
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            if (!freq[i]) {
                freq[i] = 1;
                temp.push_back(nums[i]);
                permutations(nums, temp, ans, freq);
                freq[i] = 0;
                temp.pop_back();
            }
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;
        vector<int> temp;

        vector<int> freq(nums.size(), 0);

        permutations(nums, temp, ans, freq);

        return ans;
    }
};
```
### Python Solution

```py
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        def backtrack(temp, freq):
            if len(temp) == len(nums):
                ans.append(temp[:])
                return
            for i in range(len(nums)):
                if not freq[i]:
                    freq[i] = 1
                    temp.append(nums[i])
                    backtrack(temp, freq)
                    freq[i] = 0
                    temp.pop()

        ans = []
        freq = [0] * len(nums)
        backtrack([], freq)
        return ans

```
