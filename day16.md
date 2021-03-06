## Day16

### [Odd Even Linked List](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/536/week-3-may-15th-may-21st/3331/)

---

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

**Example 1:**
```
Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL
```

**Example 2:**
```
Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
```

**Note:**

- The relative order inside both the even and odd groups should remain as it was in the input.
- The first node is considered odd, the second node even and so on ...

---
- connect all the odd nodes with other odd nodes and even nodes to other even nodes
- at the end, connect the last even node to the first odd node and remove the next node to the last odd node

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        if (!head) {
            return head;
        }
        if (!head->next) return head;
        
        ListNode* even = head;
        ListNode* oddHead = head->next;
        ListNode* odd = head->next;
        ListNode* current = head->next;
        int index = 1;
        
        while(current->next) {
            index++;
            current = current->next;
            if (index % 2 == 0) {
                even->next = current;
                even = even->next;
            }
            else {
                odd->next = current;
                odd = odd->next;
            }
        }
        even->next = oddHead;
        odd->next = nullptr;
        return head;
    }
};
```