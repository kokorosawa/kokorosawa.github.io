---
title: "576. Out of Boundary Paths"
published: 2024-04-19T23:20:08+08:00
description: "There is an m x n grid with a ball. The ball is initially at the position [startRow, startColumn]. You are allowed to move the ball to one of the four"
tags: ["LeetCode", "DFS"]
category: LeetCode
draft: false
---
# 576. Out of Boundary Paths

There is an `m x n` grid with a ball. The ball is initially at the position `[startRow, startColumn]`. You are allowed to move the ball to one of the four adjacent cells in the grid (possibly out of the grid crossing the grid boundary). You can apply **at most** `maxMove` moves to the ball.

Given the five integers `m`, `n`, `maxMove`, `startRow`, `startColumn`, return the number of paths to move the ball out of the grid boundary. Since the answer can be very large, return it **modulo** `109 + 7`.

# **Example 1:**

![Untitled](https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_1.png)

```
Input: m = 2, n = 2, maxMove = 2, startRow = 0, startColumn = 0
Output: 6
```

# **Example 2:**

![Untitled](https://assets.leetcode.com/uploads/2021/04/28/out_of_boundary_paths_2.png)

```
Input: m = 1, n = 3, maxMove = 3, startRow = 0, startColumn = 1
Output: 12
```

**Constraints:**

- `1 <= m, n <= 50`
- `0 <= maxMove <= 50`
- `0 <= startRow < m`
- `0 <= startColumn < n`

# My Solution :

一開始僅使用一般 DFS 來尋找突破邊界的路徑 
---

```cpp
class Solution {
public:
    int ans = 0;
    int findPaths(int m, int n, int maxMove, int startRow, int startColumn) {
        dfs(m, n, startRow, startColumn, maxMove);
        return ans;
    }
    
    void dfs(int m, int n, int row, int col, int move){
        if(row > m - 1 || col > n - 1 || row < 0 || col < 0){
            ans++;
            return;
        }else if(move == 0){
            return;
        }else{
            dfs(m, n, row - 1, col, move - 1);
            dfs(m, n, row + 1, col, move - 1);
            dfs(m, n, row, col + 1, move - 1);
            dfs(m, n, row, col - 1, move - 1);
        }
    }
};
```

但在繳交後發現會 TLE，原因為，，第三個維度紀錄步數

所以利用三維陣列來記錄已已經搜索過的路徑，第三個維度紀錄走到當前座標的步數有幾個方法

```cpp
int mp[51][51][51];
```

並利用 memset 來初始化陣列

```cpp
memset(mp, -1, sizeof(mp));
//     記憶體位址, 初始化值, 陣列大小
```

# Code :
---

```cpp
class Solution {
public:
    int mp[51][51][51];
    int M = 1e9 + 7;
    int findPaths(int m, int n, int maxMove, int startRow, int startColumn) {
        memset(mp, -1, sizeof(mp));
        return dfs(m, n, startRow, startColumn, maxMove);
    }
    
    int dfs(int m, int n, int row, int col, int move){
        if(row > m - 1 || col > n - 1 || row < 0 || col < 0)
            return 1;
        if(move == 0)
            return 0;
        if(mp[row][col][move] != -1) return mp[row][col][move];
        long long curr = 0;
        curr += (dfs(m, n, row - 1, col, move - 1) % M);
        curr += (dfs(m, n, row + 1, col, move - 1) % M);
        curr += (dfs(m, n, row, col + 1, move - 1) % M);
        curr += (dfs(m, n, row, col - 1, move - 1) % M);
        curr %= M;
        return mp[row][col][move] = curr;
        
    }
};
```

記得在最後記錄在陣列中的值必須 % 1000000007，

因為在題目方形極大的情況下，可能的路徑會很多，並造成 int 溢位

# Question :
---

Q : 我們在不同的路徑會多次來到同一個坐標嗎？

A : 會

Q：如果來到同一個坐標，但步數不同，屬於同一個狀態嗎？

A：不屬於，很明顯步數不同時，它們接下來的路徑也會不同。

Q：步數相同，坐標相同時，接下來的路徑數量是否一致？

A：必定一致，且在DFS搜索過程中會多次遇到之前來過的坐標、步數相同的狀態

答案[出處](https://leetcode.cn/problems/out-of-boundary-paths/solution/576-chu-jie-de-lu-jing-shu-ji-yi-hua-sou-7sg4/)
