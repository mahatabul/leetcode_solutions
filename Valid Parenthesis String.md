# 678. Valid Parenthesis String

## Company
- Yahoo  
- Amazon  
- Google  
- LinkedIn  
- Facebook  

## Difficulty
**Medium**

---

## Problem Statement

Given a string `s` containing only three types of characters: `'('`, `')'`, and `'*'`, return `true` if the string is valid.

The following rules define a valid string:
1. Any left parenthesis `'('` must have a corresponding right parenthesis `')'`.
2. Any right parenthesis `')'` must have a corresponding left parenthesis `'('`.
3. Left parenthesis `'('` must go before the corresponding right parenthesis `')'`.
4. `'*'` could be treated as:
   - A single right parenthesis `')'`, or
   - A single left parenthesis `'('`, or
   - An empty string `""`.

---

### Example 1:

**Input:**  
`s = "()"`  
**Output:**  
`true`

---

### Example 2:

**Input:**  
`s = "(*)"`  
**Output:**  
`true`

---

### Example 3:

**Input:**  
`s = "(*))"`  
**Output:**  
`true`

---

### Constraints:
- `1 <= s.length <= 100`
- `s[i]` is either `'('`, `')'`, or `'*'`

---

## Approach

1. **Stack Technique:**
   - Use two stacks:
     - One to store the indices of `'('`.
     - Another to store the indices of `'*'`.
   - When encountering `')'`, try to match it with `'('` first. If unavailable, use `'*'` as a substitute.
   - After processing the entire string, ensure that any unmatched `'('` has a corresponding `'*'` **after** it (since order matters).

2. **Time Complexity:**  
   - **O(n)** for traversing the string and processing the stacks.  
   - **O(n)** space complexity due to stack usage.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    bool checkValidString(string s) {
        stack<int> st;         // Stack for '(' positions
        stack<int> asterick;   // Stack for '*' positions

        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') {
                st.push(i);
            } else if (s[i] == '*') {
                asterick.push(i);
            } else { // s[i] == ')'
                if (!st.empty()) {
                    st.pop(); // Match with '('
                } else if (!asterick.empty()) {
                    asterick.pop(); // Use '*' as '('
                } else {
                    return false; // No match available
                }
            }
        }

        // Match remaining '(' with '*' (if '*' is after '(')
        while (!st.empty() && !asterick.empty()) {
            if (st.top() < asterick.top()) {
                st.pop();
                asterick.pop();
            } else {
                break; // Invalid if '*' is before '('
            }
        }

        return st.empty(); // Valid if no unmatched '(' remains
    }
};
```
### Python Solution

```py
class Solution:
    def checkValidString(self, s: str) -> bool:
        left_paren = []
        asterisks = []

        for i, char in enumerate(s):
            if char == '(':
                left_paren.append(i)
            elif char == '*':
                asterisks.append(i)
            else:  # char == ')'
                if left_paren:
                    left_paren.pop()
                elif asterisks:
                    asterisks.pop()
                else:
                    return False

        # Match remaining '(' with '*' if '*' appears after '('
        while left_paren and asterisks:
            if left_paren[-1] < asterisks[-1]:
                left_paren.pop()
                asterisks.pop()
            else:
                break

        return not left_paren

```

