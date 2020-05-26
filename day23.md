## Day23

### [Construct Binary Search Tree from Preorder Traversal](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/537/week-4-may-22nd-may-28th/3339/)

---

Return the root node of a binary **search** tree that matches the given `preorder` traversal.

(Recall that a binary search tree is a binary tree where for every node, any descendant of `node.left` has a value `< node.val`, and any descendant of node.right has a value > node.val.  Also recall that a preorder traversal displays the value of the node first, then traverses `node.left`, then traverses `node.right`.)

It's guaranteed that for the given test cases there is always possible to find a binary search tree with the given requirements.

**Example 1:**

```
Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
```

<img src="https://assets.leetcode.com/uploads/2019/03/06/1266.png" width="500">

**Constraints:**

- `1 <= preorder.length <= 100`
- `1 <= preorder[i] <= 10^8`
- The values of `preorder` are distinct.

---
- construct the array by root, left, right

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
    void AddValueToNode(int num, TreeNode* root){
        TreeNode* current = root;
        while(current) {
            if (current->val > num) {
                if (current->left) {
                    current = current->left;
                }
                else {
                    current->left = new TreeNode(num);
                    break;
                }
            }
            else {
                 if (current->right) {
                    current = current->right;
                }
                else {
                    current->right = new TreeNode(num);
                    break;
                }
            }
        }
    }
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        TreeNode* root = new TreeNode(preorder[0]);
        int index = 1;
        while (index < preorder.size()) {
            AddValueToNode(preorder[index], root);
            index++;
        }
        return root;
    }
};
```