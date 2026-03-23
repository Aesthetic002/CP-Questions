## Problem Link [Here](https://leetcode.com/problems/maximum-non-negative-product-in-a-matrix/description/)
## Tags #Medium #good
## Related Problems

## Topics [[Tabulation]] [[Memoization]] [[GridDP]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    int maxProductPath(vector<vector<int>>& grid) {
        int n=grid.size(),m=grid[0].size();
        vector<vector<long long>>maxP(n,vector<long long>(m,0));
        vector<vector<long long>>minP(n,vector<long long>(m,0));
        long long MOD=1000000007;
        maxP[0][0] = minP[0][0] = grid[0][0];
        for(int i=1;i<m;i++){
            maxP[0][i]=maxP[0][i-1]* grid[0][i];
            minP[0][i]=maxP[0][i];
        }

        for(int i=1;i<n;i++){
            maxP[i][0]=maxP[i-1][0]* grid[i][0];
            minP[i][0]=maxP[i][0];
        }

        for(int i=1;i<n;i++){
            for(int j=1;j<m;j++){
                long long val=grid[i][j];
                long long a=(val* maxP[i-1][j]);
                long long b=(val* minP[i-1][j]);
                long long c=(val* maxP[i][j-1]);
                long long d=(val* minP[i][j-1]);

                maxP[i][j]=max(max(a,b),max(c,d));
                minP[i][j]=min(min(a,b),min(c,d));
            }
        }
        if(maxP[n-1][m-1]<0)return -1;
        return maxP[n-1][m-1] % MOD;;


        
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