## Day5

### [First Unique Character in a String](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/3320/)

---

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**
```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

**Note:** You may assume the string contain only lowercase letters.

--- 

```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        map<char, int> m;
        for (char c: s) {
            m[c]++;
        }
        
        for (int i = 0; i < s.size(); i++) {
            if (m[s[i]] == 1) return i;
        }
        return -1;
    }
};
```