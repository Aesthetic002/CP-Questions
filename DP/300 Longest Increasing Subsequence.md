## Problem Link [Here](https://leetcode.com/problems/longest-increasing-subsequence/description/)
## Tags #Medium #good
## Related Problems

## Topics [[Memoization]] [[Tabulation]] [[Binary Search]]  [[Greedy]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int yo(vector<vector<int>>&dp,vector<int>& nums,int val,int in){

        if(in<0)return 0;

        if(dp[in][val]!=-1)return dp[in][val];

        int a=0,b=0;

  

        //Skip

        a= yo(dp,nums,val,in-1);

  

        //Not Skip

        if(nums[in]<val)

        b= 1+yo(dp,nums,nums[in],in-1);

        return dp[in][val]=max(a,b);

  

    }

    int lengthOfLIS(vector<int>& nums) {

        int maxVal = *max_element(nums.begin(), nums.end());

        int minVal = *min_element(nums.begin(), nums.end());

        int n=nums.size();

        for(auto &i:nums)i+=abs(minVal);

        vector<vector<int>>dp(n,vector<int>(maxVal+ abs(minVal)+2,-1));

        return yo(dp,nums,maxVal+abs(minVal)+1,n-1);

    }

};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {
public:
    // i = current index, prev = index of last picked element (-1 if none)
    int solve(vector<vector<int>>& dp, vector<int>& nums, int i, int prev) {
        if (i == nums.size()) return 0;

        // prev+1 used as dp index to handle -1 (shift by 1)
        if (dp[i][prev + 1] != -1) return dp[i][prev + 1];

        // Option 1: Skip nums[i]
        int skip = solve(dp, nums, i + 1, prev);

        // Option 2: Take nums[i] if it extends the subsequence
        int take = 0;
        if (prev == -1 || nums[i] > nums[prev])
            take = 1 + solve(dp, nums, i + 1, i);

        return dp[i][prev + 1] = max(skip, take);
    }

    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        // dp[i][prev+1]: i in [0,n), prev+1 in [0,n]
        vector<vector<int>> dp(n, vector<int>(n + 1, -1));
        return solve(dp, nums, 0, -1);
    }
};
```


## Approach 2

- [x] **Works**

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
    vector<int> tails;  // pile tops — always sorted

    for (int x : nums) {
        // Find leftmost pile top >= x
        auto it = lower_bound(tails.begin(), tails.end(), x);

        if (it == tails.end())
            tails.push_back(x);   // x is larger than all tops → new pile
        else
            *it = x;              // replace to maintain smallest possible top
    }

    return tails.size();  // number of piles = LIS length
}
};
```