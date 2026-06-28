---
title: "26. Remove Duplicates from Sorted Array"
published: 2022-02-23T21:27:48+08:00
description: "注意是nondecreasing order"
tags: ["LeetCode", "Array"]
category: LeetCode
draft: false
---
注意是non-decreasing order

## 完整程式碼


```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int n=nums.size();
        int left=0;
        for(int right=1;right<n;right++){
            if(nums[left]!=nums[right]){
                left++;
                nums[left]=nums[right];
            }
        }
        return left+1;
    }
};
```
