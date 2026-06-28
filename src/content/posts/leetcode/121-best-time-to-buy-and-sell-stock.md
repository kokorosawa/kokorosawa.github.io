---
title: "121. Best Time to Buy and Sell Stock"
published: 2022-02-08T00:18:42+08:00
description: "先照順序找較小值，並比較利潤最大值"
tags: ["LeetCode", "Daily"]
category: LeetCode
draft: false
---
先照順序找較小值，並比較利潤最大值

## 完整程式碼


```c
int maxProfit(int* prices, int pricesSize){
    int buy=48763,max_profit=0;
    for(int i=0;i<pricesSize;i++){
        if(buy>prices[i]){
            buy=prices[i];
        }
        int profit=prices[i]-buy;
        if(profit>max_profit) max_profit=profit;
    }
    return max_profit;
}
```
