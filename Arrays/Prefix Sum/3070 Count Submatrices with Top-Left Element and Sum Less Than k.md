## Problem Link [Here](https://leetcode.com/problems/count-submatrices-with-top-left-element-and-sum-less-than-k/description/?envType=daily-question&envId=2026-03-18)
## Tags #Medium  #good 
## Related Problems

## Topics [[Prefix Sum]]

## Solutions


## My Approach

- [x] **Works**

```cpp

class Solution {
public:
    int countSubmatrices(vector<vector<int>>& grid, int k) {
        int n=grid.size(),m=grid[0].size();
        if(grid[0][0]>k)return 0;

        int ans=1;
        for(int i=1;i<m;i++){
            grid[0][i]+=grid[0][i-1];
            if(grid[0][i]<=k)ans++;
        }
        for(int i=1;i<n;i++){
            grid[i][0]+=grid[i-1][0];
            if(grid[i][0]<=k)ans++;
        }
        for(int i=1;i<n;i++){
            for(int j=1;j<m;j++){
                grid[i][j]+=(grid[i-1][j] + grid[i][j-1])-grid[i-1][j-1];
                if(grid[i][j]<=k)ans++;
                else break;
            }
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