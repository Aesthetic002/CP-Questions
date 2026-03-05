## Problem Link [Here](https://leetcode.com/problems/longest-palindromic-subsequence/)
## Tags #Medium 
## Related Problems

## Topics [[StringDP]] [[Tabulation]] [[Memoization]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int longestPalindromeSubseq(string s) {

        string s1=s;

        reverse(s1.begin(),s1.end());

        int n=s1.size();

        vector<vector<int>>dp(n,vector<int>(n,0));

        for(int i=0;i<n;i++){

            for(int j=0;j<n;j++){

                if(s[i]==s1[j]){

                    if(j>0 && i>0)

                    dp[i][j]=1+dp[i-1][j-1];

                    else

                    dp[i][j]=1;

                }

                else{

                    int a=0,b=0;

                    if(i>0)

                    a=dp[i-1][j];

                    if(j>0)b=dp[i][j-1];

                    dp[i][j]=max(a,b);

                }

            }

        }

       return dp[n-1][n-1];

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