## Day18

### [Permutation in String](https://leetcode.com/explore/challenge/card/may-leetcoding-challenge/536/week-3-may-15th-may-21st/3333/)

---

Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.

**Example 1:**
```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**
```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
 
```

**Note:**

1. The input strings only contain lower case letters.
2. The length of both given strings is in range [1, 10,000].

---
- same question as yesterday, sliding window algorithm

```cpp
class Solution {
public:
    bool equals(int a[], int b[]) {
        for (int i = 0; i < 26; i++) {
            if (a[i] != b[i]) return false;
        }
        return true;
    }
    bool checkInclusion(string s1, string s2) {
        int a[26];
        int b[26];
        for (int i = 0; i < 26; i++) {
            a[i] = 0;
            b[i] = 0;
        }
        for (char c : s1) {
            a[c - 'a']++;
        }
        
        for (int i = 0; i < s2.size(); i++) {
            if (i >= s1.size()) {
                b[s2[i - s1.size()] - 'a']--;
            }
            b[s2[i]-'a']++;
            if (equals(a, b)) return true;
        }
        return false;
    }
};
```