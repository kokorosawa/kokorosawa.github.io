---
title: "206. Reverse Linked List"
published: 2022-02-28T23:40:29+08:00
description: "先設定三個節點變數prev=0,curr=head,prec=headnext;"
tags: ["LeetCode", "Linked List"]
category: LeetCode
draft: false
---
先設定三個節點變數prev=0,curr=head,prec=head->next;
```cpp
 while(prec){
            curr->next=prev;
            prev=curr;
            curr=prec;
            prec=prec->next;
        }
```
```cpp
curr->next=prec;
```
反轉指向前一個  
```cpp
prev=curr;
```
更新目前前一個節點  
```cpp
curr=prec;
```  
前往下一個節點  
```cpp
prec=prec->next;
```
更新下一個節點位置  
最後把節點head更新成curr(此時prec=NULL，到底了)

## 完整程式碼


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
    ListNode* reverseList(ListNode* head) {
        if(head==NULL) return head;
        ListNode* prev=0,*curr=head,*prec=head->next;
        while(prec){
            curr->next=prev;
            prev=curr;
            curr=prec;
            prec=prec->next;
        }
        curr->next=prev;
        head=curr;
        return head;
    }
};
```
