## Problem Link [Here](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/)
## Tags #Medium #good 
## Related Problems

## Topics [[Tabulation]] [[Greedy]] [[Memoization]]

## Solutions


## Greedy Approach

- [x] **Works**

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
         int n=prices.size();
        int ans=0;
        for(int i=0;i<n-1;i++){
            int diff=prices[i+1]-prices[i];
            if(diff>0)ans+=diff;
        }
        return ans;
    }
};
```


## DP Approach 

- [x] **Works**

```cpp
class Solution {
public:
    // State: index + whether we're holding a stock
    int yo(vector<vector<int>>& dp, vector<int>& prices, int in, int holding) {
        int n = prices.size();
        if (in >= n) return 0;
        if (dp[in][holding] != -1) return dp[in][holding];

        int skip = yo(dp, prices, in + 1, holding);  // do nothing today

        int act = 0;
        if (holding)
            // sell today
            act = prices[in] + yo(dp, prices, in + 1, 0);
        else
            // buy today
            act = -prices[in] + yo(dp, prices, in + 1, 1);

        return dp[in][holding] = max(skip, act);
    }

    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int>(2, -1));
        return yo(dp, prices, 0, 0);  // start with no holding
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```