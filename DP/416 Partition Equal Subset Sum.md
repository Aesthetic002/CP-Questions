## Problem Link [Here](https://leetcode.com/problems/partition-equal-subset-sum/description/)
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]] [[Memoization]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

  

    bool check(vector<int>& nums,vector<vector<int>>&dp,int index,int target){

        if(dp[index][target]!=-1)return dp[index][target];

        if(target==0)return dp[index][target]=true;

        if(index==0)return dp[index][target]=(nums[0]==target);

  

        return dp[index][target]= (check(nums,dp,index-1,target)||((target<nums[index])?(0):(check(nums,dp,index-1,target-nums[index]))));

  

    }

    bool canPartition(vector<int>& nums) {

        int n=nums.size();

        int sum=0;

        for(auto i:nums){

            sum+=i;

        }

        if(sum%2!=0)return false;

  

        int target=sum/2;

        vector<vector<int>>dp(n,vector<int>(target+1,-1));

        return check(nums,dp,nums.size()-1,target);

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