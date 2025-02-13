# 131. Palindrome Partitioning

## Company
- Apple  
- Google  
- TikTok  
- Amazon  
- Facebook  

## Difficulty
**Medium**

---

## Problem Statement

Given a string `s`, partition `s` such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of `s`.

---

### Example 1:

**Input:**  
s = "aab"  
**Output:**  
[["a","a","b"],["aa","b"]]

---

### Example 2:

**Input:**  
s = "a"  
**Output:**  
[["a"]]

---

### Constraints:
- 1 <= s.length <= 16
- s contains only lowercase English letters.

---

## Approach

1. **Backtracking Approach:**
   - We use a backtracking technique to generate all possible partitions of the string `s`.
   - For each partition, we check if the current substring is a palindrome.
   - If it is a palindrome, we add it to the current partition and recursively check the remaining part of the string.
   - If we reach the end of the string, we add the current partition to the result.

2. **Optimizations:**
   - Time Complexity: **O(n * 2^n)** (where n is the length of the string).
   - Space Complexity: **O(n)** (for the recursion stack).

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    bool ispalindrome(string s, int start, int end) {
        while (start <= end) {
            if (s[start++] != s[end--]) {
                return false;
            }
        }
        return true;
    }

    void func(int index, string s, vector<vector<string>>& ans, vector<string>& temp) {
        if (index == s.size()) {
            ans.push_back(temp);
            return;
        }

        for (int i = index; i < s.size(); i++) {
            if (ispalindrome(s, index, i)) {
                temp.push_back(s.substr(index, i - index + 1));
                func(i + 1, s, ans, temp);
                temp.pop_back();
            }
        }
    }

    vector<vector<string>> partition(string s) {
        vector<vector<string>> ans;
        vector<string> temp;
        func(0, s, ans, temp);
        return ans;
    }
};
```
### Python Solution

```py
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        def is_palindrome(s, start, end):
            while start < end:
                if s[start] != s[end]:
                    return False
                start += 1
                end -= 1
            return True

        def backtrack(index, path):
            if index == len(s):
                result.append(path[:])
                return
            for i in range(index, len(s)):
                if is_palindrome(s, index, i):
                    path.append(s[index:i+1])
                    backtrack(i + 1, path)
                    path.pop()

        result = []
        backtrack(0, [])
        return result

```        