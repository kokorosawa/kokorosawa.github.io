---
title: "389. Find the Difference"
published: 2022-02-08T00:24:12+08:00
description: "在S與T中都出現的字母次數為偶數，多出來的為奇數"
tags: ["LeetCode", "Daily"]
category: LeetCode
draft: false
---
在S與T中都出現的字母次數為偶數，多出來的為奇數  
用for檢查，最後找出出現次數為奇數的字母

## 完整程式碼


```c
char findTheDifference(char * s, char * t){
    char a[26]={0};
    int j;
    for(int i=0;*(s+i)!=NULL;i++){
        a[*(s+i)-97]++;
    }
    for(int i=0;*(t+i)!=NULL;i++){
        a[*(t+i)-97]++;
    }
    for( j=0;j<26;j++){
        if(a[j]%2==1) break;  
    }
    return j+97;
}
```
