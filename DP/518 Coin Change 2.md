## Problem Link [Here](https://leetcode.com/problems/coin-change-ii/description/)
## Tags #Medium 
## Related Problems

## Topics [[Knapsack]] [[Memoization]] [[Tabulation]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int change(int amount, vector<int>& coins) {

        int n=coins.size();

        vector<unsigned long long >dp(amount+1,0);

        dp[0]=1;

        for(int i=1;i<=n;i++){

            for(int s=coins[i-1];s<=amount;s++){

                if(s>=coins[i-1])

                dp[s]+=dp[s-coins[i-1]];

            }

        }

        return dp[amount];

    }

};
```


## Approach 1

- [ ] **Works**

```cpp

```


## Approach 2

- [ ] **Works**

```cpp

```