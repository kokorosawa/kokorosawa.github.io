---
title: "34. Find First and Last Position of Element in Sorted Array"
published: 2022-07-25T22:31:01+08:00
description: "Given an array of integers nums sorted in nondecreasing order, find the starting and ending position of a given target value."
tags: ["LeetCode", "Array"]
category: LeetCode
draft: false
---
# 34. Find First and Last Position of Element in Sorted Array

Given an array of integers `nums` sorted in non-decreasing order, find the starting and ending position of a given `target` value.

If `target` is not found in the array, return `[-1, -1]`.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]

```

**Example 3:**

```
Input: nums = [], target = 0
Output: [-1,-1]

```

**Constraints:**

- `0 <= nums.length <= 105`
- `109 <= nums[i] <= 109`
- `nums` is a non-decreasing array.
- `109 <= target <= 109`

# My Solution:



用二分搜找到數字所在位置，任一即可，並用左右指標找到開始與結束點

# Code:



```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        if(!nums.size()) return {-1,-1};
        vector<int> ans;
        int l = 0;
        int r = nums.size();
        int pos = 0;
        while(l < r){
            int mid = (l + r) / 2;
            
            if(nums[mid] > target)
                r = mid;
            else if(nums[mid] < target)
                l = mid + 1;
            else if(nums[mid] == target ){
                pos = mid;
                break;
            }
        }
        
        if(nums[pos] == target){
            l = pos;
            r = pos + 1;
            
            while(r >= 0 && r < nums.size() && nums[r] == target){
                r++;
            }
            ans.push_back(r - 1);
            
            while(l >= 0 && l < nums.size() && nums[l] == target){
                l--;
            }
            ans.push_back(l + 1);
            sort(ans.begin(),ans.end());
            return ans;
            
        }else
            return {-1,-1};
    }
};
```

C++ 有 lower_bound 可用，可依個人喜好使用
