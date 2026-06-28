---
title: "35. Search Insert Position"
published: 2022-02-11T23:25:22+08:00
description: "https://www.youtube.com/watch?v=j2JW3In9PE&t=977s&abchannel=%E5%9B%BE%E7%81%B5%E6%98%9F%E7%90%83TuringPlanet"
tags: ["LeetCode", "Binary Search"]
category: LeetCode
draft: false
---
https://www.youtube.com/watch?v=j2_JW3In9PE&t=977s&ab_channel=%E5%9B%BE%E7%81%B5%E6%98%9F%E7%90%83TuringPlanet

## 完整程式碼


```c
int searchInsert(int* nums, int numsSize, int target){
    int left=0,right=numsSize,mid;
    while(left<right){
        mid=(left+right)/2;
        if(nums[mid]>=target)
            right=mid;
        else
            left=mid+1;
    }
    return left;
}
```
