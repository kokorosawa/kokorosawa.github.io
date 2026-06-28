---
title: "62. Unique Paths"
published: 2022-08-01T15:36:03+08:00
description: "There is a robot on an m x n grid. The robot is initially located at the topleft corner (i.e., grid[0][0]). The robot tries to move to the bottomright"
tags: ["LeetCode", "DP"]
category: LeetCode
draft: false
---
# 62. Unique Paths

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return *the number of possible unique paths that the robot can take to reach the bottom-right corner*.

The test cases are generated so that the answer will be less than or equal to `2 * 109`.

**Example 1:**

![https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
Input: m = 3, n = 7
Output: 28

```

**Example 2:**

```
Input: m = 3, n = 2
Output: 3
Explanation: From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down

```

**Constraints:**

- `1 <= m, n <= 100`

# My Solution:



一開始看到走格子就想到DFS遞迴，結果TLE，有夠笨

```cpp
class Solution {
public:
    int ans = 0;
    int uniquePaths(int m, int n) {
        re(0,0,m,n);
        return ans;
    }
    
    void re(int cm,int cn,int m,int n){
        if(cm >= m || cn >= n) return;
        else if (cm == m - 1 && cn == n - 1) ans++;
        else{
            re(cm + 1,cn, m, n);
            re(cm ,cn + 1, m, n);
        }
    }
};
```

後來發現討論區在講DP，便想到DP特性，利用前面的路徑方法數來推答案，自己畫個圖，發現是還蠻簡單的題目

```cpp
class Solution {
public:
    int ans = 0;
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int> (n,1));
        for(int i = 1; i < dp.size();i++){
            for(int j = 1; j < dp[i].size(); j++){
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
};
```
