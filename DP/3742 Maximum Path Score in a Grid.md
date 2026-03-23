## Problem Link [Here](https://leetcode.com/problems/maximum-path-score-in-a-grid/description/)
## Tags #Medium #good 
## Related Problems

## Topics [[Tabulation]] [[GridDP]] [[Rolling Arrays]]

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


## Rolling Array Approach 

- [x] **Works**

```cpp
class Solution {
public:
    int maxPathScore(vector<vector<int>>& grid, int k) {
        int n = grid.size(), m = grid[0].size();

        // Only 2 rows of size m×(k+1) instead of n×m×(k+1)
        vector<vector<int>> prev(m, vector<int>(k + 1, -1));
        vector<vector<int>> curr(m, vector<int>(k + 1, -1));

        // Initialise (0,0)
        int initCost = (grid[0][0] != 0) ? 1 : 0;
        if (initCost <= k)
            prev[0][initCost] = grid[0][0];

        // Fill first row (no row above, so only left dependency)
        for (int j = 1; j < m; j++) {
            int score = grid[0][j];
            int cost  = (score != 0) ? 1 : 0;
            for (int l = cost; l <= k; l++) {
                if (prev[j-1][l-cost] != -1)
                    prev[j][l] = prev[j-1][l-cost] + score;
            }
        }

        for (int i = 1; i < n; i++) {
            // Reset curr row before filling
            for (auto& v : curr) fill(v.begin(), v.end(), -1);

            for (int j = 0; j < m; j++) {
                int score = grid[i][j];
                int cost  = (score != 0) ? 1 : 0;

                for (int l = cost; l <= k; l++) {
                    int best = -1;
                    // From row above (prev)
                    if (prev[j][l-cost] != -1)
                        best = max(best, prev[j][l-cost]);
                    // From left in same row (curr)
                    if (j > 0 && curr[j-1][l-cost] != -1)
                        best = max(best, curr[j-1][l-cost]);

                    if (best != -1)
                        curr[j][l] = best + score;
                }
            }
            swap(prev, curr); // O(1) pointer swap, no data copied
        }

        // Answer is in prev (last completed row)
        int ans = -1;
        for (int val : prev[m-1]) ans = max(ans, val);
        return ans;
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```