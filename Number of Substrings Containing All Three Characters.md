# 1358. Number of Substrings Containing All Three Characters

## Companies
- Adobe  
- DE Shaw  
- Microsoft  

## Difficulty
**Medium**

---

## Problem Statement

Given a string `s` consisting only of characters `a`, `b`, and `c`, return the number of substrings containing at least one occurrence of all these characters `a`, `b`, and `c`.

### Example 1:

**Input:**  
`s = "abcabc"`  
**Output:**  
`10`  
**Explanation:**  
The substrings containing at least one occurrence of the characters `a`, `b`, and `c` are:  
"abc", "abca", "abcab", "abcabc", "bca", "bcab", "bcabc", "cab", "cabc", and "abc" (again).

### Example 2:

**Input:**  
`s = "aaacb"`  
**Output:**  
`3`  
**Explanation:**  
The substrings containing at least one occurrence of the characters `a`, `b`, and `c` are:  
"aaacb", "aacb", and "acb".

### Example 3:

**Input:**  
`s = "abc"`  
**Output:**  
`1`

### Constraints:
- `3 <= s.length <= 5 * 10^4`
- `s` only consists of characters `a`, `b`, or `c`.

---

## Approach

The problem can be efficiently solved using a sliding window technique with two pointers. We track the last positions of the characters `a`, `b`, and `c`, and for each position `i`, we calculate the number of valid substrings that end at position `i`.

### Steps:
1. **Track Last Seen Indices:** Use a vector `c` of size 3 to store the last indices of characters `a`, `b`, and `c`.
2. **Count Valid Substrings:** For each position `i`, calculate the smallest index among the last seen indices of `a`, `b`, and `c`. This helps determine how many substrings end at `i` and contain at least one occurrence of all three characters.
3. **Update Answer:** The number of valid substrings is incremented by `(1 + mini)` where `mini` is the minimum of the last seen indices.

### Time Complexity:
- **O(n)**, where `n` is the length of the string. The algorithm processes each character of the string once.

### Space Complexity:
- **O(1)**, since the auxiliary space used is constant (only the array `c` of size 3).

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int numberOfSubstrings(string s) {
        vector<int> c(3, -1);  // Stores the last seen positions of 'a', 'b', and 'c'
        int ans = 0;

        for (int i = 0; i < s.size(); i++) {
            c[s[i] - 'a'] = i;  // Update the last seen index of the character

            // Calculate the number of valid substrings that end at position i
            int mini = min({c[0], c[1], c[2]});
            ans += (1 + mini);
        }

        return ans;
    }
};
```

### Python Solution

```python
class Solution:
    def numberOfSubstrings(self, s: str) -> int:
        c = [-1, -1, -1]  # Stores the last seen positions of 'a', 'b', and 'c'
        ans = 0

        for i, char in enumerate(s):
            c[ord(char) - ord('a')] = i  # Update the last seen index of the character

            # Calculate the number of valid substrings that end at position i
            mini = min(c)
            ans += (mini + 1)

        return ans
```  
