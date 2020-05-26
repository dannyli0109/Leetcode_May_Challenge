## Day25 Contiguous Array (Need revise)

### [Contiguous Array](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/537/week-4-may-22nd-may-28th/3341/)

---

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**
```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

**Note:** The length of the given binary array will not exceed 50,000.

---
- keep track of the count and the index, if the same count appears twice, the sum is zero
- the result will the the maximum length of `i - m[count]`


```cpp
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        map<int, int> m;
        m[0] = -1;
        int count = 0;
        int result = 0;
        for (int i = 0; i < nums.size(); i++) {
            count += nums[i] == 0 ? -1 : 1;
            if (m.find(count) != m.end()) {
                result = max(result, i - m[count]);
            }
            else {
                m[count] = i;
            }
        }
        
        return result;
    }
};
```