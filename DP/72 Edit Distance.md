## Problem Link [Here](https://leetcode.com/problems/edit-distance/)
## Tags #Medium 
## Related Problems

## Topics [[StringDP]] [[Memoization]] [[Tabulation]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int yo(string word1, string word2,vector<vector<int>>&dp,int i,int j){

        if(j<0)return i+1;

        if(i<0)return j+1;

        if(dp[i][j]!=-1)return dp[i][j];

        if(word1[i]==word2[j]){

            return dp[i][j]=yo(word1,word2,dp,i-1,j-1);

        }

        else{

            //insert

            int a=1+yo(word1,word2,dp,i,j-1);

  

            //delete

            int b=1+yo(word1,word2,dp,i-1,j);

  

            //replace

  

            int c=1+ yo(word1,word2,dp,i-1,j-1);

            return dp[i][j]=min(a,min(b,c));

        }

    }

    int minDistance(string word1, string word2) {

        int n=word1.size(),m=word2.size();

        vector<vector<int>>dp(n,vector<int>(m,-1));

        return yo(word1,word2,dp,n-1,m-1);

    }

};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {

public:

    int minDistance(string word1, string word2) {

        int n=word1.size(),m=word2.size();

        vector<vector<int>>dp(n+1,vector<int>(m+1,0));

        for(int i=0;i<=m;i++)dp[0][i]=i;

        for(int i=0;i<=n;i++)dp[i][0]=i;

  

        for(int i=1;i<=n;i++){

            for(int j=1;j<=m;j++){

                if(word1[i-1]==word2[j-1])

                dp[i][j]=dp[i-1][j-1];

                else{

                    dp[i][j]=1+min(dp[i][j-1],min(dp[i-1][j],dp[i-1][j-1]));

                }

            }

        }

        return dp[n][m];

    }

};
```


## Approach 2

- [ ] **Works**

```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {

        int n = word1.size();
        int m = word2.size();

        vector<int> prev(m+1), curr(m+1);

        for(int j=0;j<=m;j++) prev[j]=j;

        for(int i=1;i<=n;i++){
            curr[0]=i;

            for(int j=1;j<=m;j++){

                if(word1[i-1]==word2[j-1])
                    curr[j]=prev[j-1];
                else
                    curr[j]=1+min({curr[j-1],prev[j],prev[j-1]});
            }

            prev=curr;
        }

        return prev[m];
    }
};
```