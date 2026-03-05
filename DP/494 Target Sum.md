## Problem Link [Here](https://leetcode.com/problems/target-sum/)
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]] [[Knapsack]] [[Memoization]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int findTargetSumWays(vector<int>& nums, int target) {

        int n=nums.size();

        int sum=0;

        for(auto i:nums)sum+=i;

        if(((sum+target)%2!=0)||(sum<abs(target)))return 0;

        int yo=(sum+target)/2;

  

        vector<vector<int>>dp(n+1,vector<int>(yo+1,0));

  

        dp[0][0]=1;

  

        for(int i=1;i<=n;i++){

            for(int s=0;s<=yo;s++){

                //Not take

  

                dp[i][s]=dp[i-1][s];

  

                //take

  

                if(s>=nums[i-1])

                dp[i][s]+=dp[i-1][s-nums[i-1]];

            }

        }

        return dp[n][yo];

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