---
title: "240. Search a 2D Matrix II"
published: 2022-07-25T22:34:58+08:00
description: "Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:"
tags: ["LeetCode", "Array"]
category: LeetCode
draft: false
---
# 240. Search a 2D Matrix II

Write an efficient algorithm that searches for a value `target` in an `m x n` integer matrix `matrix`. This matrix has the following properties:

- Integers in each row are sorted in ascending from left to right.
- Integers in each column are sorted in ascending from top to bottom.

**Example 1:**

![https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg](https://assets.leetcode.com/uploads/2020/11/24/searchgrid2.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true

```

**Example 2:**

![https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg](https://assets.leetcode.com/uploads/2020/11/24/searchgrid.jpg)

```
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
Output: false

```

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= n, m <= 300`
- `109 <= matrix[i][j] <= 109`
- All the integers in each row are **sorted** in ascending order.
- All the integers in each column are **sorted** in ascending order.
- `109 <= target <= 109`

# My Solution:

用 for 迴圈將每層跑一次二元搜尋法，若每層的最後一個小於 target ，便可知此層無答案，同理若每層的第一個大於 target ，也可知此層無答案 ， 增加搜索效率

# Code :

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        for(int i = 0;i < matrix.size(); i++){
            int l = 0;
            int r = matrix[i].size();
            if(matrix[i].back() < target)
                continue;
            if(matrix[i][0] > target)
                break;
            while(l<r){
                int mid = (l + r)/2;
                if(matrix[i][mid] == target)
                    return true;
                else if(matrix[i][mid] > target)
                    r = mid;
                else if(matrix[i][mid] < target)
                    l = mid + 1; 
            }
        }
        return false;
    }
};
```

![](https://cdn.discordapp.com/attachments/965654631344635934/1000695952232947792/unknown.png)

不用呼叫函式就是慢啦

Leetcode 不知道為什麼呼叫較快，有夠怪

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        for(int i = 0;i < matrix.size(); ++i){
            int l = 0;
            int r = matrix[i].size() - 1;
            if(matrix[i].back() < target)
                continue;
            if(matrix[i][0] > target)
                break;
           if(search(matrix[i],target)){
                return 1;
            }
        }
        return 0;
    }
    
    bool search(vector<int> &arr,int t){
        int l = 0;
        int r = arr.size()-1;
         while(l <= r){
            int mid = (l + r)/2;
            if(arr[mid] > t)
                r = mid - 1;
            else if(arr[mid] < t)
                l = mid + 1; 
            else if(arr[mid] == t)
                return 1;
        }
        return arr[r] == t;
    }
};
```

![Untitled](https://cdn.discordapp.com/attachments/920347870555701330/1001130912584581170/unknown.png)
