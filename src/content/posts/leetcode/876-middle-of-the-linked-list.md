---
title: "876. Middle of the Linked List"
published: 2022-02-26T00:39:40+08:00
description: "Discuss上的最佳解："
tags: ["LeetCode", "Linked List"]
category: LeetCode
draft: false
---
Discuss上的最佳解：  
一次走兩個head：slow,fast  
slow一次走一步，fast一次走兩步。
最終fast先到NULL，slow停在mid+1的位子

## 完整程式碼


```cpp
//mine:
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
    ListNode* middleNode(ListNode* head) {
        int count=0,mid;
        ListNode* temp=head;
        while(head){
            count++;
            head=head->next;
        }
        mid=(count/2)+1;
        count=0;
        while(temp){
            count++;
            if(count==mid) break;
            temp=temp->next;
        }
        return temp;
    }
};
//Discuss
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *slow = head, *fast = head;
        while (fast && fast->next) {
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
};
```
