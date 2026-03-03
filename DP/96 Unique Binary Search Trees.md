## Problem Link [Here](https://leetcode.com/problems/unique-binary-search-trees/description/?envType=problem-list-v2&envId=binary-tree)
## Tags #Medium 
## Related Problems 

## Topics [[Tabulation]] [[Memoization]] [[Math]]

## Solutions


## My Approach (Memoization)

- [x] **Works**

```cpp
class Solution {

public:

    long long yo(int n,vector<long long>&dp){

        if(n==0)return dp[0]=1;

        if(n==1)return dp[1]=1;

        if(dp[n]!=-1)return dp[n];

        long long ans=0;

        for(int i=1;i<=n;i++){

            long long l=yo(i-1,dp);

            long long r=yo(n-i,dp);

            ans+=l*r;

  

        }

        return dp[n]=ans;

    }

    int numTrees(int n) {

        vector<long long>dp(n+1,-1);

        return yo(n,dp);

    }

};
```


## Approach 1(Tabulation)

- [x] **Works**

```cpp
class Solution {
public:
    int numTrees(int n) {
        vector<long long> dp(n+1, 0);

        // base cases
        dp[0] = 1;
        dp[1] = 1;

        // build up
        for (int nodes = 2; nodes <= n; nodes++) {
            for (int root = 1; root <= nodes; root++) {
                dp[nodes] += dp[root-1] * dp[nodes-root];
            }
        }

        return dp[n];
    }
};

```


## Approach 2(Math-Catalan Numbers)

- [x] **Works**

```cpp
class Solution {
public:
    int numTrees(int n) {
        long long C = 1;   // C0 = 1

        for (int i = 0; i < n; i++) {
            C = C * 2 * (2*i + 1) / (i + 2);
        }

        return (int)C;    // LeetCode n ≤ 19 fits in int
    }
};

```