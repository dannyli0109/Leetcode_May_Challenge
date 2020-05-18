## Day17

### [Find All Anagrams in a String](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/536/week-3-may-15th-may-21st/3332/)

---

Given a string **s** and a **non-empty** string **p**, find all the start indices of **p**'s anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than `20,100`.

The order of output does not matter.

**Example 1:**
```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**
```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

---


```cpp
class Solution {
public:
    bool equals(int a[], int b[]) {
        for (int i = 0; i < 26; i++) {
            if (a[i] != b[i]) return false;
        }
        return true;
    }
    vector<int> findAnagrams(string s, string p) {
        vector<int> results;
        int a[26];
        int b[26];
        for (int i = 0; i < 26; i++) {
            a[i] = 0;
            b[i] = 0;
        }
        for (int i = 0; i < p.size(); i++) {
            a[p[i] - 'a']++;
        }
        
        for (int i = 0; i < s.size(); i++) {
            if (i >= p.size()) {
                if (equals(a, b)) results.push_back(i - p.size());
                b[s[i - p.size()] - 'a']--;
            }
            b[s[i] - 'a']++;
        }
        if (equals(a, b)) results.push_back(s.size() - p.size());
        return results;
    }
};
```