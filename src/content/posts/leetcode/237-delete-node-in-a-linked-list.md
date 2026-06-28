---
title: "237. Delete Node in a Linked List"
published: 2022-02-26T17:00:11+08:00
description: "讓目標數字變的跟下一個節點的數字一樣，在跳過第二個一樣的數字"
tags: ["LeetCode", "Linked List"]
category: LeetCode
draft: false
---
讓目標數字變的跟下一個節點的數字一樣，在跳過第二個一樣的數字

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
    void deleteNode(ListNode* node) {
        node->val=node->next->val;
        node->next=node->next->next;
    }
};
```
