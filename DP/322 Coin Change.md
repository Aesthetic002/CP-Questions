## Problem Link [Here](https://leetcode.com/problems/coin-change/description/)
## Tags #Medium 
## Related Problems

## Topics [[Knapsack]] [[Tabulation]] [[Memoization]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

  

    int coinChange(vector<int>& coins, int amt) {

        int n=coins.size();

        vector<long long>dp(amt+1,INT_MAX);

        dp[0]=0;

        for(int i=1;i<=n;i++){

            for(int j=coins[i-1];j<=amt;j++){

                    dp[j]=min(dp[j],1+dp[j-coins[i-1]]);

            }

        }

        if(dp[amt]==INT_MAX)return -1;

        return dp[amt];

    }

};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {

public:

  

    int coinChange(vector<int>& coins, int amt) {

        int n=coins.size();

        vector<vector<long long>>dp(n+1,vector<long long>(amt+1,INT_MAX));

        dp[0][0]=0;

        for(int i=1;i<=n;i++){

            for(int j=0;j<=amt;j++){

                //not take

                dp[i][j]=dp[i-1][j];

  

                //take

                if(j>=coins[i-1]){

                    dp[i][j]=min(dp[i][j],1+dp[i][j-coins[i-1]]);

                }

            }

        }

        if(dp[n][amt]==INT_MAX)return -1;

        return dp[n][amt];

    }

};
```


## Approach 2

- [ ] **Works**

```cpp

```