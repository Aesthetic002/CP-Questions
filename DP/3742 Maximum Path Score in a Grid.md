## Problem Link [Here]()
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int maxPathScore(vector<vector<int>>& grid, int k) {

        int n=grid.size(),m=grid[0].size();

        vector<vector<vector<int>>> dp(

            n, vector<vector<int>>(m, vector<int>(k + 1, INT_MIN))

        );

        dp[0][0][0]=0;

        for(int i=0;i<n;i++){

            for(int j=0;j<m;j++){

                int score=grid[i][j];

                int cost=(grid[i][j]==0)?0:1;

                for(int c =cost;c<=k;c++ ){

                    if(i>0 && dp[i-1][j][c-cost]!=INT_MIN){

                        dp[i][j][c]=max(dp[i][j][c],dp[i-1][j][c-cost]+score);

                    }

                    if(j>0 && dp[i][j-1][c-cost]!=INT_MIN){

                        dp[i][j][c]=max(dp[i][j][c],dp[i][j-1][c-cost]+score);

                    }

                }

            }

        }

        int ans=-1;

        for(auto i:dp[n-1][m-1]){

            ans=max(ans,i);

        }

  

        return ans;

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