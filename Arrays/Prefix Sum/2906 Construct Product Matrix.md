## Problem Link [Here](https://leetcode.com/problems/construct-product-matrix/description/?envType=daily-question&envId=2026-03-24)
## Tags #Medium 
## Related Problems

## Topics [[Prefix Sum]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    vector<vector<int>> constructProductMatrix(vector<vector<int>>& grid) {
        int n=grid.size(),m=grid[0].size();
        vector<int>pref(n*m),suf(n*m); // 00 0 01 1 02 2 03 3 04 4 10 5 11 6 12 7 13 8 14 9
        long long MOD=12345;
        pref[0]=1;suf[(n*m)-1]=1;
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(i==n-1 && j==m-1)break;
                int ind= (m * i) +j;
                pref[ind+1]=((long long)pref[ind]*(long long)grid[i][j])%MOD;
            }
        }
        for(int i=n-1;i>=0;i--){
            for(int j=m-1;j>=0;j--){
                if(i==0 && j==0)break;
                int ind= (m * i) +j;
                suf[ind-1]=((long long)suf[ind]*(long long)grid[i][j])%MOD;
            }
        }

        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                int ind= (m * i) +j;
                grid[i][j]=(suf[ind]*pref[ind])%MOD;
            }
        }
        return grid;

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