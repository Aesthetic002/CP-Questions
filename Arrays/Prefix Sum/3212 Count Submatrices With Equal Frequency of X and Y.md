## Problem Link [Here](https://leetcode.com/problems/count-submatrices-with-equal-frequency-of-x-and-y/description/)
## Tags #Medium 
## Related Problems

## Topics [[Prefix Sum]] 

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    int numberOfSubmatrices(vector<vector<char>>& grid) {
        int n=grid.size(),m=grid[0].size();
        vector<vector<vector<int>>> g(n,vector<vector<int>>(m,vector<int>(2,0)));
        int ans=0;
        if(grid[0][0]=='X')g[0][0]={1,0};
        else if(grid[0][0]=='Y')g[0][0]={0,1};
        for(int i=1;i<n;i++){
            if(grid[i][0]=='X')g[i][0]={1,0};
            else if(grid[i][0]=='Y')g[i][0]={0,1};
            g[i][0][0]+=g[i-1][0][0];
            g[i][0][1]+=g[i-1][0][1];
            if(g[i][0][0] && g[i][0][0]==g[i][0][1])ans++;
        }
        for(int i=1;i<m;i++){
            if(grid[0][i]=='X')g[0][i]={1,0};
            else if(grid[0][i]=='Y')g[0][i]={0,1};
            g[0][i][0]+=g[0][i-1][0];
            g[0][i][1]+=g[0][i-1][1];
            if(g[0][i][0] && g[0][i][0]==g[0][i][1])ans++;
        }
        for(int i=1;i<n;i++){
            for(int j=1;j<m;j++){
                if(grid[i][j]=='X')g[i][j]={1,0};
                else if(grid[i][j]=='Y')g[i][j]={0,1};
                g[i][j][0]+=g[i-1][j][0] + g[i][j-1][0] - g[i-1][j-1][0];
                g[i][j][1]+=g[i-1][j][1] + g[i][j-1][1] - g[i-1][j-1][1];
                if(g[i][j][0] && g[i][j][0]==g[i][j][1])ans++;

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