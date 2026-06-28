---
title: "136. Single Number"
published: 2022-02-10T00:47:39+08:00
description: "利用xor把每個都xor一遍"
tags: ["LeetCode", "Array"]
category: LeetCode
draft: false
---
利用xor把每個都xor一遍  
xor特性:
```c
0^0=0
0^1=1
1^0=1
1^1=0
```
出現過兩次經過xor就會變為0，而0^某數＝某數  
https://medium.com/@hyWang/xor-位元運算子-1c25b4ae15fb

## 完整程式碼


```c
int singleNumber(int* nums, int numsSize){
    int result=*(nums);
    for(int i=1;i<numsSize;i++){
        result^=*(nums+i);
    }
    return result;
}
```
