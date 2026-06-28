---
title: "118. Pascal's Triangle"
published: 2022-07-19T16:46:46+08:00
description: "Given an integer numRows, return the first numRows of Pascal's triangle."
tags: ["LeetCode", "Array"]
category: LeetCode
draft: false
---
# 118. Pascal's Triangle

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

**Example 1:**

```
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

```

**Example 2:**

```
Input: numRows = 1
Output: [[1]]

```

**Constraints:**

- `1 <= numRows <= 30`

# My Solution:
先宣告二維陣列，並在第一層放入 1 ， 且之後每層前後都放入 1 ，

並建立 temp 值， temp = dp[ i - 1 ][ j - 1 ] + dp[ i - 1 ][ j ]，

最後推入該層陣列

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> dp(numRows);
        dp[0].push_back(1);
        
        for(int i = 1; i < dp.size(); i++){
            dp[i].push_back(1);
            for(int j = 1; j < i ; j++){
                int temp = dp[i - 1][j - 1] + dp[i - 1][j];
                dp[i].push_back(temp);
            }
            dp[i].push_back(1);
        }
        return dp;
    }
};
```
