# 57. Insert Interval

## Company
- Google  
- Amazon  
- LinkedIn  
- Facebook  
- Robinhood  

## Difficulty
**Medium**

---

## Problem Statement

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` represent the start and the end of the `ith` interval, and `intervals` is sorted in ascending order by `starti`. You are also given an interval `newInterval = [start, end]` that represents the start and end of another interval.

Insert `newInterval` into `intervals` such that `intervals` is still sorted in ascending order by `starti` and does not have any overlapping intervals (merge overlapping intervals if necessary).

Return `intervals` after the insertion.

**Note:** You don't need to modify `intervals` in-place. You can make a new array and return it.

---

### Example 1:

**Input:**  
`intervals = [[1,3],[6,9]], newInterval = [2,5]`  
**Output:**  
`[[1,5],[6,9]]`

---

### Example 2:

**Input:**  
`intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]`  
**Output:**  
`[[1,2],[3,10],[12,16]]`  
**Explanation:**  
Because the new interval `[4,8]` overlaps with `[3,5],[6,7],[8,10]`.

---

### Constraints:
- `0 <= intervals.length <= 10^4`
- `intervals[i].length == 2`
- `0 <= starti <= endi <= 10^5`
- `intervals` is sorted by `starti` in ascending order.
- `newInterval.length == 2`
- `0 <= start <= end <= 10^5`

---

## Approach

1. **Iterate through `intervals`**:
   - Add all intervals that end before `newInterval` starts.
   - Merge overlapping intervals by updating `newStart` and `newEnd`.
   - Add all intervals that start after `newInterval` ends.

2. **Time Complexity**:  
   - Sorting is not needed since `intervals` is already sorted.  
   - We traverse the list once, so the solution runs in **O(n)** time.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals,
                               vector<int>& newInterval) {

        int newStart = newInterval[0], newEnd = newInterval[1],
            n = intervals.size();

        vector<vector<int>> ans;

        int i = 0;
        while (i < n and intervals[i][1] < newStart) {
            ans.push_back({intervals[i][0], intervals[i][1]});
            i++;
        }

        while (i < n and intervals[i][0] <= newEnd) {
            newStart = min(intervals[i][0], newStart);
            newEnd = max(intervals[i][1], newEnd);
            i++;
        }
        ans.push_back({newStart, newEnd});

        while (i < n) {
            ans.push_back(intervals[i]);
            i++;
        }

        return ans;
    }
};
```

### Python Solution

```py
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        result = []
        i = 0
        n = len(intervals)
        
        while i < n and intervals[i][1] < newInterval[0]:
            result.append(intervals[i])
            i += 1
        
        while i < n and intervals[i][0] <= newInterval[1]:
            newInterval[0] = min(intervals[i][0], newInterval[0])
            newInterval[1] = max(intervals[i][1], newInterval[1])
            i += 1
        
        result.append(newInterval)
        
        while i < n:
            result.append(intervals[i])
            i += 1
        
        return result
```