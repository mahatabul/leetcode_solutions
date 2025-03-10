# 860. Lemonade Change

## Company
- Apple  
- Amazon  
- Atlassian  

## Difficulty
**Easy**

---

## Problem Statement

At a lemonade stand, each lemonade costs `$5`. Customers are standing in a queue to buy from you and order one at a time (in the order specified by `bills`). Each customer will only buy one lemonade and pay with either a `$5`, `$10`, or `$20` bill. You must provide the correct change to each customer so that the net transaction is that the customer pays `$5`.

Note that you do not have any change in hand at first.

Given an integer array `bills` where `bills[i]` is the bill the `i-th` customer pays, return `true` if you can provide every customer with the correct change, or `false` otherwise.

### Example 1:

**Input:**  
`bills = [5,5,5,10,20]`  
**Output:**  
`true`  
**Explanation:**  
From the first 3 customers, we collect three `$5` bills in order.  
From the fourth customer, we collect a `$10` bill and give back a `$5`.  
From the fifth customer, we give a `$10` bill and a `$5` bill.  
Since all customers got correct change, we output `true`.

### Example 2:

**Input:**  
`bills = [5,5,10,10,20]`  
**Output:**  
`false`  
**Explanation:**  
From the first two customers in order, we collect two `$5` bills.  
For the next two customers in order, we collect a `$10` bill and give back a `$5` bill.  
For the last customer, we cannot give the change of `$15` back because we only have two `$10` bills.  
Since not every customer received the correct change, the answer is `false`.

### Constraints:
- `1 <= bills.length <= 10^5`
- `bills[i]` is either `5`, `10`, or `20`.

---

## Approach

1. **Greedy Strategy:**
   - Maintain counters for `$5` and `$10` bills.
   - Traverse the `bills` array and handle transactions accordingly:
     - If a customer pays with `$5`, increase the count of `$5` bills.
     - If a customer pays with `$10`, check if there is a `$5` bill available for change. If yes, decrease `$5` count and increase `$10` count; otherwise, return `false`.
     - If a customer pays with `$20`, try to give one `$10` and one `$5` as change. If not possible, try to give three `$5` bills. If neither is possible, return `false`.

---

## Solutions

### C++ Solution

```cpp
class Solution {
public:
    bool lemonadeChange(vector<int>& bills) {
        int five = 0, ten = 0;
        
        for (int bill : bills) {
            if (bill == 5) {
                five++;
            } else if (bill == 10) {
                if (five == 0) return false;
                five--;
                ten++;
            } else { // bill == 20
                if (ten > 0 && five > 0) {
                    ten--;
                    five--;
                } else if (five >= 3) {
                    five -= 3;
                } else {
                    return false;
                }
            }
        }
        return true;
    }
};
```

### Python Solution

```python
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        five, ten = 0, 0
        
        for bill in bills:
            if bill == 5:
                five += 1
            elif bill == 10:
                if five == 0:
                    return False
                five -= 1
                ten += 1
            else:  # bill == 20
                if ten > 0 and five > 0:
                    ten -= 1
                    five -= 1
                elif five >= 3:
                    five -= 3
                else:
                    return False
        
        return True
```

