## Day1

### [Jewels and Stones](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/3317/)

---

You're given strings `J` representing the types of stones that are jewels, and `S` representing the stones you have.  Each character in `S` is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in `J` are guaranteed distinct, and all characters in `J` and `S` are letters. Letters are case sensitive, so `"a"` is considered a different type of stone from `"A"`.

**Example 1:**
```
Input: J = "aA", S = "aAAbbbb"
Output: 3
```

**Example 2:**
```
Input: J = "z", S = "ZZ"
Output: 0
```

**Note:**

- `S` and `J` will consist of letters and have length at most 50.
- The characters in `J` are distinct.

---

- use a set or a map

```cpp
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        set<char> jewels;
        int count = 0;
        for (char j : J) {
            jewels.insert(j);
        }
        
        for (char s : S) {
            if (jewels.find(s) != jewels.end()) count++;
        }
        return count;
    }
};
```

```cpp
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        unordered_map<char, int> dict;
        int count = 0;
        for (int i = 0; i < J.size(); i++){
            dict.insert({J[i], 1});
        } 
        for (int i = 0; i < S.size(); i++)  {
            if (dict[S[i]] > 0) count++;
        }
        return count;
    }
    // test
};
```
