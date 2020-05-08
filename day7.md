## Day7

### [Cousins in Binary Tree](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/3322/)

---

In a binary tree, the root node is at depth `0`, and children of each depth `k` node are at depth `k+1`.

Two nodes of a binary tree are cousins if they have the same depth, but have **different parents**.

We are given the `root` of a binary tree with unique values, and the values `x` and `y` of two different nodes in the tree.

Return `true` if and only if the nodes corresponding to the values `x` and `y` are cousins.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/12/q1248-01.png)

```
Input: root = [1,2,3,4], x = 4, y = 3
Output: false
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2019/02/12/q1248-02.png)

```
Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2019/02/13/q1248-03.png)

```
Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false
```

**Note:**

1. The number of nodes in the tree will be between `2` and `100`.
2. Each node has a unique integer value from `1` to `100`.

---

- find x and y recursively and return their parents and depth
- if the depth are the same and the value of the parents are different, return true

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
    bool isCousins(TreeNode* root, int x, int y) {
        pair<TreeNode*, int> r1 = find(root, x);
        pair<TreeNode*, int> r2 = find(root, y);
        return r1.first && r2.first && r1.first->val != r2.first->val && r1.second == r2.second;
    }
    
    pair<TreeNode*, int> find(TreeNode* root, int x, int depth = 0, TreeNode* parent = nullptr) {
        if (root) {
            if (root->val == x) return pair<TreeNode*, int> {parent, depth};
            pair<TreeNode*, int> left = find(root->left, x, depth + 1, root);
            if (left.second > -1) return left;
            pair<TreeNode*, int> right = find(root->right, x, depth + 1, root);
            if (right.second > -1) return right;       
        }  
        return pair<TreeNode*, int> {nullptr, -1};
    }
};
```