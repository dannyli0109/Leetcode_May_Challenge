## Day9

### [Valid Perfect Square](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/535/week-2-may-8th-may-14th/3324/)

---

Given a positive integer num, write a function which returns True if num is a perfect square else False.

**Note: Do not** use any built-in library function such as `sqrt`.

**Example 1:**
```
Input: 16
Output: true
```

**Example 2:**
```
Input: 14
Output: false
```

---
- keep multiply by two until the square is greater than the target, then adjust by -1 until it hits the target

```cpp
class Solution {
public:
    bool isPerfectSquare(int num) {
        if (num == 0 || num == 1) return true;
        long n = 2;
        while(n * n != num) {
           if (n * n > num && (n-1) * (n-1) < num) return false;
            if (n * n < num) {
                n *= 2;
            }
            else {
                n--;
            }
        }
        return true;
    }
};
```