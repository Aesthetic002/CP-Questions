## Problem Link [Here](https://leetcode.com/problems/wildcard-matching/description/)
## Tags #Hard 
## Related Problems

## Topics [[StringDP]] [[Memoization]] [[Tabulation]]

## Solutions


## Recursive Approach

- [ ] **Works**

```cpp
class Solution {
public:

    bool yo(string &s, string &p, int i, int j){

        if(i < 0 && j < 0) return true;

        if(j < 0) return false;

        if(i < 0){
            for(int k = 0; k <= j; k++){
                if(p[k] != '*') return false;
            }
            return true;
        }

        if(p[j] == s[i] || p[j] == '?')
            return yo(s,p,i-1,j-1);

        if(p[j] == '*')
            return yo(s,p,i,j-1) || yo(s,p,i-1,j);

        return false;
    }

    bool isMatch(string s, string p) {
        return yo(s,p,s.size()-1,p.size()-1);
    }
};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {
public:

    bool yo(vector<vector<int>>&dp,string &s, string &p,int i,int j){
        if(i<0 && j<0)return true;
        if(j<0)return false;
        if(i<0){
            for(int k=0;k<=j;k++){
                if(p[k]!='*')return false;
            }
            return true;
        }
        if(dp[i][j]!=-1)return dp[i][j];
        if(s[i]==p[j] || p[j]=='?'){
            return dp[i][j]=yo(dp,s,p,i-1,j-1);
        }

        if(p[j]=='*'){
            return dp[i][j]=(yo(dp,s,p,i-1,j) || yo(dp,s,p,i,j-1));
        }
        return dp[i][j]=false;
    }
    bool isMatch(string s, string p) {
       
        int n=s.size(),m=p.size();
         vector<vector<int>>dp(n,vector<int>(m,-1));
        return yo(dp,s,p,n-1,m-1);
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```