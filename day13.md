## Day13

### [Remove K Digits](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/535/week-2-may-8th-may-14th/3328/)

---

Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

**Note:**
- The length of num is less than 10002 and will be ≥ k.
- The given num does not contain any leading zero.

**Example 1:**

```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

**Example 2:**
```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```

**Example 3:**
```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

---
- the general rule being if `num[i] > num[i + 1]`, remove the digit, if there's leading zeros, remove the zeros.

```cpp
class Solution {
public:
    string removeKdigits(string num, int k) {
        int i = 0;
        while(k > 0 && i < num.size() - 1) {
            if (num.size() < 2) return "0";
            if (num[i] > num[i + 1]) {
                num = num.substr(0, i) + num.substr(i + 1);
                k--;
                if (i > 0) {
                    i--;       
                }
            }
            else {
                i++;
            }
            
            while(num[0] == '0' && num.size() > 1) {
                num = num.substr(1);
            }
        }
        while (k > 0) {
            if (num.size() == 0) return "0";
            num = num.substr(0, num.size() - 1);
            k--;
        }
        if (num.size() == 0) return "0";
        return num;
    }
};
```