## Day20

### [Kth Smallest Element in a BST](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/536/week-3-may-15th-may-21st/3335/)

---

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

**Example 1:**
```
Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
```

**Example 2:**
```
Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
```

**Follow up:**
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

**Constraints:**

- The number of elements of the BST is between `1` to `10^4`.
- You may assume `k` is always valid, `1 ≤ k ≤ BST's total elements`.

---
- Because it is a binary search tree, it is sorted, so the array will be sorted if we put left -> root -> right and we recursively go down the tree, at the end we get the sorted array 
- output with array[k + 1]


```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> makeArray(TreeNode* root) {
        if (!root) return {};         
        vector<int> l;
        vector<int> r;
        if (root->left) {
            l = makeArray(root->left);    
        }
        
        if (root->right) {
            r = makeArray(root->right);
        }
        l.push_back(root->val);
        l.insert(l.end(), r.begin(), r.end());
        return l;
    }
    int kthSmallest(TreeNode* root, int k) {
        return makeArray(root)[k - 1];
    }
};
```