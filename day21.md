## Day21

### [Sort Characters By Frequency](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/537/week-4-may-22nd-may-28th/3337/)

---

Given a string, sort it in decreasing order based on the frequency of characters.

**Example 1:**
```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

**Example 2:**
```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```

**Example 3:**
```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

---
- make a map of frequency
- use that to construct and array of pair of character, frequency
- sort the array by frequency
- reconstruct the string using the array

```cpp
class Solution {
public:
    string frequencySort(string s) {
        map<char, int> map;
        for (char c : s) {
          map[c]++;
        }
        
        vector<pair<char, int>> chars;
        for (auto it = map.begin(); it != map.end(); it++) {
            chars.push_back({it->first, it->second});
        }
        
        sort(chars.begin(), chars.end(), [](pair<char, int> p1, pair<char, int> p2) {
            return p2.second < p1.second;
        });
        
        string newS = "";
        for (pair<char, int> p : chars) {
            newS += string(p.second, p.first);
        }
        return newS;
    }
};
```