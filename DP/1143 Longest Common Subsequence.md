## Problem Link [Here](https://leetcode.com/problems/longest-common-subsequence/description/)
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]] [[Memoization]] [[StringDP]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

  

    int yo(int i1,int i2,string &text1, string &text2,vector<vector<int>>&dp){

        if(i1==-1 || i2==-1)return 0;

        if(dp[i1][i2]!=-1)return dp[i1][i2];

  

        if(text1[i1]==text2[i2]){

            return dp[i1][i2]= 1 + yo(i1-1,i2-1,text1,text2,dp);

        }

        return dp[i1][i2]=max(yo(i1-1,i2,text1,text2,dp),yo(i1,i2-1,text1,text2,dp));

    }

    int longestCommonSubsequence(string text1, string text2) {

        int i1=text1.size()-1,i2=text2.size()-1;

        vector<vector<int>>dp(i1+1,vector<int>(i2+1,-1));

        return yo(i1,i2,text1,text2,dp);

    }

};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {

public:

  

    int longestCommonSubsequence(string text1, string text2) {

        int i1=text1.size()-1,i2=text2.size()-1;

        vector<vector<int>>dp(i1+1,vector<int>(i2+1,0));

        for(int i=0;i<dp.size();i++){

            for(int j=0;j<dp[0].size();j++){

                if(text1[i]==text2[j]){

                    if(i>0 && j>0){

                        dp[i][j]=dp[i-1][j-1]+1;

                    }

                    else{

                        dp[i][j]=1;

                    }

                }

                else {

                    int a=0,b=0;

                    if(i>0){

                        a=dp[i-1][j];

                    }

                    if(j>0){

                        b=dp[i][j-1];

                    }

                    dp[i][j]=max(a,b);

                }

            }

        }

        return dp[i1][i2];

    }

};
```


## Approach 2

- [ ] **Works**

```cpp

```