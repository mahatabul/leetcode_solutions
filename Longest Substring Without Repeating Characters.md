# 3. Longest Substring Without Repeating Characters

## Company
- Uber  
- Zoho  
- Apple  
- Adobe  
- Yahoo  
- Amazon  
- Google  
- VMware  
- Oracle  
- Paypal  
- Intuit  
- Yandex  
- Spotify  
- Samsung  
- Facebook  
- JPMorgan  
- Microsoft  
- Bloomberg  
- Salesforce  
- Goldman Sachs  
- Walmart Global Tech  

## Difficulty
**Medium**

---

## Problem Statement

Given a string `s`, find the length of the longest substring without repeating characters.

### Example 1:

Input: s = "abcabcbb" Output: 3 Explanation: The answer is "abc", with the length of 3.


### Example 2:

Input: s = "bbbbb" Output: 1 Explanation: The answer is "b", with the length of 1.


### Example 3:

Input: s = "pwwkew" Output: 3 Explanation: The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.


### Constraints:
- `0 <= s.length <= 5 * 10^4`
- `s` consists of English letters, digits, symbols, and spaces.

---

## Approach

1. **Sliding Window Technique**:
   - Use two pointers (`l` and `r`) to maintain a sliding window representing the current substring without repeating characters.
   - Use a hash map to keep track of the frequency of characters within the current window.

2. **Expanding and Contracting the Window**:
   - Expand the window by moving the `r` pointer to the right and adding the character to the hash map.
   - If the character count exceeds 1 (indicating a repetition), move the `l` pointer to the right to shrink the window until all characters are unique.

3. **Track the Maximum Length**:
   - At each step, update the maximum length of the substring found so far.

4. **Time Complexity**:
   - The algorithm runs in **O(n)** as each character is processed at most twice (once for addition and once for removal).

5. **Space Complexity**:
   - The space complexity is **O(k)**, where `k` is the number of unique characters in the input string.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int l = 0, r = 0, maxlength = 0;
        map<char, int> hmap;

        while (r < s.size()) {
            hmap[s[r]]++;

            while (hmap[s[r]] > 1) {
                hmap[s[l]]--;
                l++;
            }

            maxlength = max(maxlength, r - l + 1);
            r++;
        }

        return maxlength;
    }
};
```
### Python Solution

```py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        l, maxlength = 0, 0
        hmap = {}

        for r in range(len(s)):
            hmap[s[r]] = hmap.get(s[r], 0) + 1

            while hmap[s[r]] > 1:
                hmap[s[l]] -= 1
                if hmap[s[l]] == 0:
                    del hmap[s[l]]
                l += 1

            maxlength = max(maxlength, r - l + 1)

        return maxlength
```        