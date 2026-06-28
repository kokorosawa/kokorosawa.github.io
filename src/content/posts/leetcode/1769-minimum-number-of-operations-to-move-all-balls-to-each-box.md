---
title: "1769. Minimum Number of Operations to Move All Balls to Each Box"
published: 2022-03-13T02:33:47+08:00
description: "https://www.uj5u.com/ruanti/325642.html"
tags: ["LeetCode", "Array"]
category: LeetCode
draft: false
---
https://www.uj5u.com/ruanti/325642.html  
  
use two step to count ,one is from left,another is right  
ops is the int to count the step to the current position,  
and count is int to count how many ball with ops.
```
index      0 1 2  
num        1 1 0  
time1(L)   0 1 3  
time2(R)   1 0 0  
ans        1 1 3
```

## 完整程式碼


```cpp
class Solution {
public:
    vector<int> minOperations(string boxes) {
        int n=boxes.length();
        vector<int> ans;
        int count=0,ops=0;//from left
        for(int i=0;i<n;i++){
            ops+=count;
            ans.push_back(ops);
            if(boxes[i]=='1') count++;
        }
        count=0,ops=0;//from right
        for(int i=n-1;i>=0;i--){
            ops+=count;
            ans[i]+=ops;
            if(boxes[i]=='1') count++;
        }
        return ans;
    }
};
```
