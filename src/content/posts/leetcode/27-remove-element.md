---
title: "27. Remove Element"
published: 2022-02-08T00:18:42+08:00
description: "icount是要調換保留的數字在前面的index"
tags: ["LeetCode", "Daily"]
category: LeetCode
draft: false
---
i-count是要調換保留的數字在前面的index


要回傳的是要印出這個陣列的前幾個

## 完整程式碼


```c
int removeElement(int* nums, int numsSize, int val){
    int count=0;
    for(int i=0;i<numsSize;i++){
        if(nums[i]==val) count++;
        else nums[i-count]=nums[i];
    }
    return numsSize-count;
}
```
