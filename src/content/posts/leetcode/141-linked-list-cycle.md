---
title: "141. Linked List Cycle"
published: 2022-03-08T22:02:58+08:00
description: "ues the same way like last time,declared two pointer slow and fast"
tags: ["LeetCode", "Linked List"]
category: LeetCode
draft: false
---
ues the same way like last time,declared two pointer slow and fast
faster go two step per time,slow go one step per time,  
have to careful about the condition of while,  
must be
```cpp
fast->next&&fast->next->next;
```
can't not be like is:  
```cpp
slow->nxet&&fast->next->next;
```
cuz most of time they point to the different node

## 完整程式碼


```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head) return false;
        ListNode *slow=head,*fast=head;
        while(fast->next&&fast->next->next){
            slow=slow->next;
            fast=fast->next->next;
            if(slow==fast) return true;
        }
        return false;
    }
};
```
