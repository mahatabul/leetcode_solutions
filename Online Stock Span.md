# 901. Online Stock Span

## Companies
- Adobe  
- Amazon  
- Bloomberg  

## Difficulty
**Medium**

---

## Problem Statement

Design an algorithm that collects daily price quotes for some stock and returns the span of that stock's price for the current day.

The span of the stock's price in one day is the maximum number of consecutive days (starting from that day and going backward) for which the stock price was less than or equal to the price of that day.

For example:
- If the prices of the stock in the last four days are `[7,2,1,2]` and today's price is `2`, then the span of today is `4` because starting from today, the price of the stock was less than or equal to `2` for 4 consecutive days.
- If the prices of the stock in the last four days are `[7,34,1,2]` and today's price is `8`, then the span of today is `3` because starting from today, the price of the stock was less than or equal to `8` for 3 consecutive days.

### Implementation Details

Implement the `StockSpanner` class:

- `StockSpanner()`: Initializes the object of the class.
- `int next(int price)`: Returns the span of the stock's price given that today's price is `price`.

### Example:

**Input:**  
```plaintext
["StockSpanner", "next", "next", "next", "next", "next", "next", "next"]
[[], [100], [80], [60], [70], [60], [75], [85]]

Output:

[null, 1, 1, 1, 2, 1, 4, 6]
```

**Explanation:**
```cpp
StockSpanner stockSpanner = new StockSpanner();
stockSpanner.next(100); // return 1
stockSpanner.next(80);  // return 1
stockSpanner.next(60);  // return 1
stockSpanner.next(70);  // return 2
stockSpanner.next(60);  // return 1
stockSpanner.next(75);  // return 4
stockSpanner.next(85);  // return 6
```

### Constraints:

    1 <= price <= 10^5
    At most 10^4 calls will be made to next.

## Approach

The problem can be efficiently solved using a monotonic decreasing stack.

### Key Steps:

1. **Use a Stack:** Store pairs of (price, index) to efficiently calculate the span.
2. **Check for Consecutive Smaller Prices:**  
    - If the stack is not empty and the top element’s price is **less than or equal** to the current price, pop elements from the stack.
3. **Calculate the Span:**  
    - If the stack is empty, the span is the entire length seen so far.
    - Otherwise, the span is the difference between the current index and the index at the top of the stack.
4. **Push the Current Price and Index onto the Stack.**

### Time Complexity:

- **O(1) Average Per Query**: Each element is pushed and popped from the stack at most once, making it **O(n) amortized** for `n` queries.

### Space Complexity:

- **O(n)**, in the worst case, if prices are in strictly decreasing order.

---

## Solution Code

### C++ Solution

```cpp
class StockSpanner {
public:
    stack<pair<int, int>> st;
    int idx;

    StockSpanner() {
        idx = -1;
    }

    int next(int price) {
        idx += 1;
        while (!st.empty() && st.top().first <= price) {
            st.pop();
        }
        
        int ans = idx - (st.empty() ? -1 : st.top().second);
        st.push({price, idx});
        return ans;
    }
};
```

### Python Solution

```python
class StockSpanner:
    def __init__(self):
        self.stack = []  # Stores (price, index)
        self.idx = -1

    def next(self, price: int) -> int:
        self.idx += 1
        
        while self.stack and self.stack[-1][0] <= price:
            self.stack.pop()
        
        ans = self.idx - (self.stack[-1][1] if self.stack else -1)
        self.stack.append((price, self.idx))
        
        return ans
```

