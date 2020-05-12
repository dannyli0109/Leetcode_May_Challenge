## Day11

### [Flood Fill](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/535/week-2-may-8th-may-14th/3326/)

---

An `image` is represented by a 2-D array of integers, each integer representing the pixel value of the image (from 0 to 65535).

Given a coordinate `(sr, sc)` representing the starting pixel (row and column) of the flood fill, and a pixel value `newColor`, "flood fill" the image.

To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color as the starting pixel), and so on. Replace the color of all of the aforementioned pixels with the newColor.

At the end, return the modified image.

**Example 1:**
```
Input: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
Output: [[2,2,2],[2,2,0],[2,0,1]]
Explanation: 
From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected 
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
```

**Note:**

- The length of `image` and `image[0]` will be in the range `[1, 50]`.
- The given starting pixel will satisfy `0 <= sr < image.length` and `0 <= sc < image[0].length`.
- The value of each color in `image[i][j]` and `newColor` will be an integer in `[0, 65535]`.

---
- bfs search all four directions each time

```cpp
class Solution {
public:
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        int rows = image.size();
        int cols = image[0].size();
        int dirX[] = {0, 1, 0, -1};
        int dirY[] = {-1, 0, 1, 0};
        int sourceColor = image[sr][sc];
        queue<vector<int>> coordinates;
        coordinates.push({sr, sc});
        
        while(coordinates.size() > 0) {
            int n = coordinates.size();
            for (int i = 0; i < n; i++) {
                vector<int> currentCoordinate = coordinates.front();
                coordinates.pop();
                int cr = currentCoordinate[0];
                int cc = currentCoordinate[1];
                if (image[cr][cc] == sourceColor && sourceColor != newColor) {
                    image[cr][cc] = newColor;
                    
                    for (int i = 0; i < 4; i++) {
                        int nr = cr + dirY[i];
                        int nc = cc + dirX[i];
                        if (nr >= 0 && nr < rows && nc >= 0 && nc < cols) {
                            coordinates.push({nr, nc});
                        }
                    }
                }
            }
        }
        return image;
    }
};
```