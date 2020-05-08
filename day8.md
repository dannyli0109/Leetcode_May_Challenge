## Day8

### [Check If It Is a Straight Line](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/535/week-2-may-8th-may-14th/3323/)

---

You are given an array `coordinates`, `coordinates[i] = [x, y]`, where `[x, y]` represents the coordinate of a point. Check if these points make a straight line in the XY plane.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/10/15/untitled-diagram-2.jpg)

```
Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/10/09/untitled-diagram-1.jpg)

```
Input: coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
Output: false
```

**Constraints:**

- `2 <= coordinates.length <= 1000`
- `coordinates[i].length == 2`
- `-10^4 <= coordinates[i][0], coordinates[i][1] <= 10^4`
- `coordinates` contains no duplicate point.

---

```cpp
class Solution {
public:
    bool checkStraightLine(vector<vector<int>>& coordinates) {
        // by = ax + c
        int x1 = coordinates[0][0];
        int x2 = coordinates[1][0];
        int y1 = coordinates[0][1];
        int y2 = coordinates[1][1];
        int a;
        int b;
        int c;
        
        if (x2 == x1) {
            b = 0;
            a = 1;
            c = -a * x1 + b * y1;
        }
        else {
            a = (y2 - y1) / (x2 - x1);
            b = 1;
            c = -a * x1 + b * y1;
        }
        
        for (vector<int> coordinate : coordinates) {
            int x = coordinate[0];
            int y = coordinate[1];
            if (y * b != a * x  + c) {
                return false;
            }
        }
        return true;
    }
};
```