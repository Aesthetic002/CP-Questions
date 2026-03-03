## Problem Link [Here](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)
## Tags #Medium 
## Related Problems

## Topics [[Memoization]] [[Tabulation]] [[StringDP]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int findLength(vector<int>& text1, vector<int>& text2) {

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

            }

        }

        int maxi=0;

        for(int i=0;i<dp.size();i++){

            for(int j=0;j<dp[0].size();j++){

                maxi=max(maxi,dp[i][j]);

            }

        }

        return maxi;

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