## Day14

### [Implement Trie (Prefix Tree)](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/535/week-2-may-8th-may-14th/3329/)

---

Implement a trie with `insert`, `search`, and `startsWith` methods.

**Example:**
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

**Note:**

- You may assume that all inputs are consist of lowercase letters `a-z`.
- All inputs are guaranteed to be non-empty strings.

--- 
- use tree structure with 26 nodes to represent all the characters

```cpp
class Trie {
public:
    Trie* root[26];
    bool end;
    /** Initialize your data structure here. */
    Trie() {
        end = false;
        for (int i = 0; i < 26; i++) {
            root[i] = nullptr;
        }
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        Trie* current = this;
        for (int i = 0; i < word.size(); i++) {
            if (!current->root[word[i] - 'a']) {
                Trie* t = new Trie();
                current->root[word[i] - 'a'] = t;
            }
            current = current->root[word[i] - 'a'];
        }
        current->end = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        Trie* current = this;
        for (int i = 0; i < word.size(); i++) {
            if (!current->root[word[i] - 'a']) return false;
            current = current->root[word[i] - 'a'];
        }
        if (current->end) return true;
        return false;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        Trie* current = this;
        for (int i = 0; i < prefix.size(); i++) {
            if (!current->root[prefix[i] - 'a']) return false;
            current = current->root[prefix[i] - 'a'];
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```