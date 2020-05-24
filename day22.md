## Day22

### [Interval List Intersections](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/537/week-4-may-22nd-may-28th/3338/)

---

Given two lists of **closed** intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

(Formally, a closed interval `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.  The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.  For example, the intersection of [1, 3] and [2, 4] is [2, 3].)

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

```
Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
Reminder: The inputs and the desired output are lists of Interval objects, and not arrays or lists.
```

**Note:**

1. 0 <= A.length < 1000
2. 0 <= B.length < 1000
3. 0 <= A[i].start, A[i].end, B[i].start, B[i].end < 10^9

---
- having to pointers point to each of the list, if the and increment with the lower upper bound

```cpp
class Solution {
public:
    vector<vector<int>> intervalIntersection(vector<vector<int>>& A, vector<vector<int>>& B) {
        int i = 0;
        int j = 0;
        vector<vector<int>> result;
        
        while (i < A.size() && j < B.size()) {
            int low = max(A[i][0], B[j][0]);
            int high = min(A[i][1], B[j][1]);
            
            if (low <= high) {
                result.push_back({low, high});
            }
            
            if (A[i][1] < B[j][1]) {
                i++;
            }
            else {
                j++;
            }
        }
        return result;
    }
};
```