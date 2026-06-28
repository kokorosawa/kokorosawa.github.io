---
title: "53. Maximum Subarray"
published: 2022-02-25T21:55:36+08:00
description: "每加一個就和現在已知最大值比對，若sum小於0，sum=0"
tags: ["LeetCode", "Array"]
category: LeetCode
draft: false
---
每加一個就和現在已知最大值比對，若sum小於0，sum=0

## 完整程式碼


```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int max_sum=INT_MIN;
        int sum=0;
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
            max_sum=std::max(max_sum,sum);
            if(sum<0) sum=0;
        }
        return max_sum;
    }
};
```
