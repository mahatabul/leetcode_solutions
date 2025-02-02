# 435. Non-overlapping Intervals

## Company
- Oracle  
- Amazon  
- Google  
- Samsung  
- Facebook  
- Microsoft  
- Expedia Group  
- NCR Corporation  

## Difficulty
**Medium**

---

## Problem Statement

Given an array of intervals `intervals` where `intervals[i] = [start_i, end_i]`, return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

Note that intervals which only touch at a point are non-overlapping. For example, `[1, 2]` and `[2, 3]` are non-overlapping.

### Example 1:

**Input:**  
`intervals = [[1,2],[2,3],[3,4],[1,3]]`  
**Output:**  
`1`  
**Explanation:**  
`[1,3]` can be removed and the rest of the intervals are non-overlapping.

### Example 2:

**Input:**  
`intervals = [[1,2],[1,2],[1,2]]`  
**Output:**  
`2`  
**Explanation:**  
You need to remove two `[1,2]` to make the rest of the intervals non-overlapping.

### Example 3:

**Input:**  
`intervals = [[1,2],[2,3]]`  
**Output:**  
`0`  
**Explanation:**  
You don't need to remove any of the intervals since they're already non-overlapping.

### Constraints:
- `1 <= intervals.length <= 10^5`
- `intervals[i].length == 2`
- `-5 * 10^4 <= start_i < end_i <= 5 * 10^4`

---

## Approach

1. **Greedy Algorithm:**
   - Sort intervals based on their end times.
   - Initialize `endTime` to the end of the first interval.
   - Iterate through the sorted intervals:
     - If the start time of the current interval is less than `endTime`, increment the count of intervals to remove.
     - Otherwise, update `endTime` to the current interval's end time.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        if (intervals.empty())
            return 0;

        sort(intervals.begin(), intervals.end(),
             [](const vector<int>& a, const vector<int>& b) {
                 return a[1] < b[1];
             });

        int ans = 0;
        int endTime = intervals[0][1];
        for (int i = 1; i < intervals.size(); i++) {
            if (intervals[i][0] < endTime) {
                ans++;
            } else {
                endTime = intervals[i][1];
            }
        }

        return ans;
    }
};
```

### Python Solution

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        if not intervals:
            return 0

        intervals.sort(key=lambda x: x[1])
        end_time = intervals[0][1]
        count = 0

        for i in range(1, len(intervals)):
            if intervals[i][0] < end_time:
                count += 1
            else:
                end_time = intervals[i][1]

        return count
```

