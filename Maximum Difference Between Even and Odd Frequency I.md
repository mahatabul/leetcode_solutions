# 3442. Maximum Difference Between Even and Odd Frequency I

## Company


## Difficulty
**Easy**

---

## Problem Statement

You are given a string `s` consisting of lowercase English letters. Your task is to find the maximum difference between the frequency of two characters in the string such that:

- One of the characters has an even frequency in the string.
- The other character has an odd frequency in the string.

Return the maximum difference, calculated as the frequency of the character with an odd frequency minus the frequency of the character with an even frequency.

### Example 1:

**Input:**  
`s = "aaaaabbc"`  
**Output:**  
`3`  
**Explanation:**  
- The character `'a'` has an odd frequency of `5`, and `'b'` has an even frequency of `2`.  
- The maximum difference is `5 - 2 = 3`.

### Example 2:

**Input:**  
`s = "abcabcab"`  
**Output:**  
`1`  
**Explanation:**  
- The character `'a'` has an odd frequency of `3`, and `'c'` has an even frequency of `2`.  
- The maximum difference is `3 - 2 = 1`.

### Constraints:
- `3 <= s.length <= 100`
- `s` consists only of lowercase English letters.
- `s` contains at least one character with an odd frequency and one with an even frequency.

---

## Approach

1. **Frequency Counting:**  
   - Use a hash map to count the frequency of each character in the string `s`.

2. **Identifying Odd and Even Frequencies:**  
   - Iterate through the frequency map.  
   - Track the maximum odd frequency and the minimum even frequency.

3. **Calculating the Result:**  
   - Return the difference: `max_odd - min_even`.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int maxDifference(string s) {
        int even = INT_MAX, odd = INT_MIN;
        map<char, int> mp;

        for (int i = 0; i < s.size(); i++) {
            mp[s[i]]++;
        }

        for (auto it : mp) {
            if (it.second & 1) {
                odd = max(odd, it.second);
            } else {
                even = min(even, it.second);
            }
        }

        return (odd - even);
    }
};
```

### Python Solution

```python
class Solution:
    def maxDifference(self, s: str) -> int:
        from collections import Counter
        freq = Counter(s)
        
        odd = float('-inf')
        even = float('inf')

        for count in freq.values():
            if count % 2 == 1:
                odd = max(odd, count)
            else:
                even = min(even, count)

        return odd - even
```

