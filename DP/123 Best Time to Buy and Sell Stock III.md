## Problem Link [Here](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)
## Tags #Hard 
## Related Problems

## Topics [[Tabulation]] [[Memoization]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    int yo(vector<int>& prices,vector<vector<vector<int>>>&dp,int in,int hold,int num){
        int n=prices.size();
        if(in>=n || num>=2)return 0;
        int a=INT_MIN,b=INT_MIN;
        if(dp[in][hold][num]!=-1)return dp[in][hold][num];
        //skip
        a=yo(prices,dp,in+1,hold,num);

        //buy
        if(hold==0){
            b= -prices[in]+yo(prices,dp,in+1,1,num);
        }

        //sell
        else{
            b= +prices[in]+yo(prices,dp,in+1,0,num+1);
        }

        return dp[in][hold][num]=max(a,b);

    }
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        vector<vector<vector<int>>>dp(n,vector<vector<int>>(2,vector<int>(2,-1)));
        return yo(prices,dp,0,0,0);
    }
};
```


## Greedy Approach 

- [x] **Works**

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
    int buy1 = INT_MIN, sell1 = 0;
    int buy2 = INT_MIN, sell2 = 0;

    for (int price : prices) {
        buy1  = max(buy1,  -price);
        sell1 = max(sell1,  buy1  + price);
        buy2  = max(buy2,   sell1 - price);
        sell2 = max(sell2,  buy2  + price);
    }
    return sell2;
}
};
```


## Approach 2

- [ ] **Works**

```cpp

```