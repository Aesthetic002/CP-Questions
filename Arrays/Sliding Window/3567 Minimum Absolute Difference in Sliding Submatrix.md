## Problem Link [Here](https://leetcode.com/problems/minimum-absolute-difference-in-sliding-submatrix/)
## Tags #Medium 
## Related Problems

## Topics [[Sliding Window]] 

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    vector<vector<int>> minAbsDiff(vector<vector<int>>& grid, int k) {
        map<int,int>mp;
        int n=grid.size(),m=grid[0].size();
        vector<vector<int>>ans(n-k+1,vector<int>(m-k+1,0));
        
        for(int i=0;i<(n-k+1);i++){
            for(int a=i;(a-i)<k;a++){
                for(int j=0;j<k;j++){
                    mp[grid[a][j]]++;
                }
            }
            int yo=INT_MAX;
            for(auto it = mp.begin(); next(it) != mp.end(); ++it){
                yo = min(yo, next(it)->first - it->first);
            }
            if(yo==INT_MAX)yo=0;
            ans[i][0]=yo;
            for(int j=1;j<(m-k+1);j++){
                for(int s=i;(s-i)<k;s++){
                    mp[grid[s][j-1]]--;
                    if(mp[grid[s][j-1]]==0)mp.erase(grid[s][j-1]);
                    mp[grid[s][j+k-1]]++;
                }
                int yo=INT_MAX;
                for(auto it = mp.begin(); next(it) != mp.end(); ++it){
                    yo = min(yo, next(it)->first - it->first);
                }
                if(yo==INT_MAX)yo=0;
                ans[i][j]=yo;
            }
            mp.clear();
        }
        return ans;
    }
};
```


## Editorial Approach 1

- [x] **Works**

```cpp
class Solution {
public:
    vector<vector<int>> minAbsDiff(vector<vector<int>>& grid, int k) {
        int m = grid.size(), n = grid[0].size();
        vector<vector<int>> res(m - k + 1, vector<int>(n - k + 1));
        for (int i = 0; i + k <= m; i++) {
            for (int j = 0; j + k <= n; j++) {
                vector<int> kgrid;
                for (int x = i; x < i + k; x++) {
                    for (int y = j; y < j + k; y++) {
                        kgrid.push_back(grid[x][y]);
                    }
                }
                int kmin = INT_MAX;
                sort(kgrid.begin(), kgrid.end());
                for (int t = 1; t < kgrid.size(); t++) {
                    if (kgrid[t] == kgrid[t - 1]) {
                        continue;
                    }
                    kmin = min(kmin, kgrid[t] - kgrid[t - 1]);
                }
                if (kmin != INT_MAX) {
                    res[i][j] = kmin;
                }
            }
        }
        return res;
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```