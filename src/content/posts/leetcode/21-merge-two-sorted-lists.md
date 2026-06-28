---
title: "21. Merge Two Sorted Lists"
published: 2022-02-09T20:00:27+08:00
description: "原理：兩兩比較，指向較小的，並把較小指向下一個節點，大的不動，一直執行比較直到其中一個為NULL"
tags: ["LeetCode", "Linked List"]
category: LeetCode
draft: false
---
原理：兩兩比較，指向較小的，並把較小指向下一個節點，大的不動，一直執行比較直到其中一個為NULL  
錯誤一：return curr 但在while中curr起點中一直在變
```c
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode* curr=(struct ListNode*)malloc(sizeof(struct ListNode));
    while(l1&&l2){
        if(l1->val>l2->val){
            curr->next=l2;
            l2=l2->next;
        }else{
            curr->next=l1;
            l1=l1->next;
        }
        curr=curr->next;
    }
    if(l1==NULL) curr=l2->next;
    if(l2==NULL) curr=l1->next;
    
    return curr;
}
```  
且
```c
    if(l1==NULL) curr=l2->next;
    if(l2==NULL) curr=l1->next;
```
應改為
```
    if(l1!=NULL) curr->next=l1;
    if(l2!=NULL) curr->next=l2;
```
錯誤二：return  會多出前面暫時的curr＊所指向head的值，出現未定義行為
```c
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode* curr=(struct ListNode*)malloc(sizeof(struct ListNode));
    struct ListNode*result=curr->next;
    while(l1&&l2){
        if(l1->val>l2->val){
            curr->next=l2;
            l2=l2->next;
        }else{
            curr->next=l1;
            l1=l1->next;
        }
        curr=curr->next;
    }
    if(l1!=NULL) curr->next=l1;
    if(l2!=NULL) curr->next=l2;
    
    return result;
}
``` 
結果：先設兩個節點指標，第一次if決定L1還是L2當第一個節點，之後用while來檢查其中之一是否到NULL，其中一個到NULL後，後面全接上未結束的list
```c
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode* p,*t;
    if(l1==NULL) return l2;
    if(l2==NULL) return l1;
    if(l1->val>l2->val){
        p=l2;
        l2=l2->next;
    }else{
        p=l1;
        l1=l1->next;
    }
    t=p;
    while(l1&&l2){
       if(l1->val>l2->val){
            p->next=l2;
            l2=l2->next;
        }else{
            p->next=l1;
            l1=l1->next;
        }
        p=p->next;
    }
    if(l1) p->next=l1;
    if(l2) p->next=l2;
    
    return t;
}
```

## 完整程式碼


```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    struct ListNode* p,*t;
    if(l1==NULL) return l2;
    if(l2==NULL) return l1;
    if(l1->val>l2->val){
        p=l2;
        l2=l2->next;
    }else{
        p=l1;
        l1=l1->next;
    }
    t=p;
    while(l1&&l2){
       if(l1->val>l2->val){
            p->next=l2;
            l2=l2->next;
        }else{
            p->next=l1;
            l1=l1->next;
        }
        p=p->next;
    }
    if(l1) p->next=l1;
    if(l2) p->next=l2;
    
    return t;
}
```
