## Day3

### [Ransom Note](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/3318/)

---

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

**Note:**

You may assume that both strings contain only lowercase letters.

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

---

- use a map 

```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        map<char, int> note;
        for (char c : magazine) {
            note[c]++;
        }
        
        for (char c : ransomNote) {
            if(note[c] > 0) {
                note[c] --;
            }
            else {
                return false;
            }
        }
        return true;
    }
};
```