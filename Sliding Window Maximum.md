# 239. Sliding Window Maximum

## Company
- IBM  
- OYO  
- Yelp  
- HSBC  
- MSCI  
- Uber  
- Intel  
- Tesla  
- Quikr  
- Cisco  
- PayTM  
- Adobe  
- Apple  
- Quora  
- Amazon  
- Oracle  
- PayPal  
- Splunk  
- Google  
- Soroco  
- Practo  
- Twilio  
- TikTok  
- VMware  
- Dropbox  
- Expedia  
- Twitter  
- Samsung  
- Walmart  
- Virtusa  
- Nagarro  
- Citadel  
- DE Shaw  
- LinkedIn  
- Razorpay  
- Flipkart  
- HCL Tech  
- MobiKwik  
- Hashedin  
- Facebook  
- DoorDash  
- Mathworks  
- Two Sigma  
- Instacart  
- Lifesight  
- Microsoft  
- Cognizant  
- ByteDance  
- Bloomberg  
- Databricks  
- Innovaccer  
- Salesforce  
- Incedo Inc.  
- Wadhwani AI  
- Booking.com  
- Mercer Mettl  
- EPAM Systems  
- Akuna Capital  
- Goldman Sachs  
- Morgan Stanley  
- American Express  
- Cruise Automation  
- Cashfree Payments  
- Accion Labs India  
- Byte Bonding Tech  
- Emerson Electric Co.  
- Hughes Systique Corporation (HSC)  

## Difficulty
**Hard**

---

## Problem Statement

You are given an array of integers `nums`, and there is a sliding window of size `k` which moves from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return the maximum sliding window.

### Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3 Output: [3,3,5,5,6,7] Explanation: Window position Max

[1 3 -1] -3 5 3 6 7 3 1 [3 -1 -3] 5 3 6 7 3 1 3 [-1 -3 5] 3 6 7 5 1 3 -1 [-3 5 3] 6 7 5 1 3 -1 -3 [5 3 6] 7 6 1 3 -1 -3 5 [3 6 7] 7


### Example 2:

Input: nums = [1], k = 1 Output: [1]


### Constraints:
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`

---

## Approach

1. **Deque Data Structure**:
   - Use a deque to store the indices of elements in the sliding window.
   - Maintain the deque in decreasing order of element values.

2. **Sliding Window Logic**:
   - For each element in the array, remove indices that are out of the sliding window.
   - Remove elements from the deque that are smaller than or equal to the current element.
   - Add the current element's index to the deque.
   - Record the maximum element in the window after processing at least `k` elements.

3. **Time Complexity**:
   - The algorithm runs in **O(n)** because each element is pushed and popped from the deque at most once.

4. **Space Complexity**:
   - The space complexity is **O(k)**, where `k` is the size of the sliding window.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> dq;
        vector<int> ans;

        for (int i = 0; i < nums.size(); i++) {
            // Remove indices that are out of the sliding window
            if (!dq.empty() && dq.front() <= i - k) {
                dq.pop_front();
            }

            // Remove smaller elements in deque
            while (!dq.empty() && nums[dq.back()] <= nums[i]) {
                dq.pop_back();
            }

            // Add current element index to deque
            dq.push_back(i);

            // Record maximum for the current window
            if (i >= k - 1) {
                ans.push_back(nums[dq.front()]);
            }
        }

        return ans;
    }
};
```

### Python Solution

```py
from collections import deque

class Solution:
    def maxSlidingWindow(self, nums, k):
        dq = deque()
        ans = []

        for i in range(len(nums)):
            # Remove indices out of sliding window
            if dq and dq[0] <= i - k:
                dq.popleft()

            # Remove smaller elements in deque
            while dq and nums[dq[-1]] <= nums[i]:
                dq.pop()

            # Add current element index to deque
            dq.append(i)

            # Record maximum for the current window
            if i >= k - 1:
                ans.append(nums[dq[0]])

        return ans
```        