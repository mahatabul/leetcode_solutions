# 1423. Maximum Points You Can Obtain from Cards

## Company
- Adobe  
- Google  
- Amazon  

## Difficulty
**Medium**

---

## Problem Statement

There are several cards arranged in a row, and each card has an associated number of points. The points are given in the integer array `cardPoints`.

In one step, you can take one card from the beginning or from the end of the row. You have to take exactly `k` cards.

Your score is the sum of the points of the cards you have taken.

Given the integer array `cardPoints` and the integer `k`, return the maximum score you can obtain.

### Example 1:
Input: cardPoints = [1,2,3,4,5,6,1], k = 3 Output: 12 Explanation: The optimal strategy is to take the three cards on the right, giving a final score of 1 + 6 + 5 = 12.

### Example 2:
Input: cardPoints = [2,2,2], k = 2 Output: 4 Explanation: Regardless of which two cards you take, your score will always be 4.

### Example 3:
Input: cardPoints = [9,7,7,9,7,7,9], k = 7 Output: 55 Explanation: You have to take all the cards. Your score is the sum of points of all cards.


### Constraints:
- `1 <= cardPoints.length <= 10^5`
- `1 <= cardPoints[i] <= 10^4`
- `1 <= k <= cardPoints.length`

---

## Approach

1. **Initial Window**:
   - Sum up the first `k` cards to get the initial score.
2. **Sliding Window Technique**:
   - Start replacing the leftmost card in the current sum with the rightmost card (from the back of the array) to explore all possibilities.
   - Track the maximum score across all windows.
3. **Time Complexity**:
   - The algorithm runs in **O(k)** for the initial sum and **O(k)** for the sliding window, making the total time complexity **O(k)**.
4. **Space Complexity**:
   - The algorithm uses **O(1)** extra space.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int maxScore(vector<int>& cp, int k) {
        int ans = 0;
        int l = k - 1, r = cp.size() - 1;
        for (int i = 0; i < k; i++) {
            ans += cp[i];
        }

        int curr = ans;

        while (k != 0) {
            curr -= cp[l];
            l--;
            curr += cp[r];
            r--;
            k--;

            ans = max(ans, curr);
        }

        return ans;
    }
};

```

### Python Solution

```py
class Solution:
    def maxScore(self, cardPoints, k):
        ans = sum(cardPoints[:k])
        curr = ans
        l, r = k - 1, len(cardPoints) - 1

        while k != 0:
            curr -= cardPoints[l]
            l -= 1
            curr += cardPoints[r]
            r -= 1
            k -= 1

            ans = max(ans, curr)

        return ans
```
