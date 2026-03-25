## Problem Link [Here](https://leetcode.com/problems/equal-sum-grid-partition-i/description/?envType=daily-question&envId=2026-03-25)
## Tags #Medium 
## Related Problems

## Topics [[Prefix Sum]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    bool canPartitionGrid(vector<vector<int>>& grid) {
        int n=grid.size(),m=grid[0].size();
        vector<long long>yo1,yo2;
        for(int i=0;i<n;i++){
            long long pd=0;
            for(int j=0;j<m;j++){
                pd=pd+grid[i][j];
            }
            yo1.push_back(pd);
        }

        for(int j=0;j<m;j++){
            long long pd=0;
            for(int i=0;i<n;i++){
                pd=pd+grid[i][j];
            }
             yo2.push_back(pd);
        }

        vector<long long>pref1(n),suf1(n);
        pref1[0]=yo1[0];
        suf1[n-1]=0;

        for(int i=1;i<n-1;i++){
            pref1[i]=pref1[i-1]+yo1[i];
        }
        for(int i=n-1;i>0;i--){
            suf1[i-1]=suf1[i]+yo1[i];
        }

        for(int i=0;i<n-1;i++){
            if(suf1[i] && pref1[i] && pref1[i]==suf1[i])return true;
        }

        vector<long long>pref2(m),suf2(m);
        pref2[0]=yo2[0];
        suf2[m-1]=0;

        for(int i=1;i<m-1;i++){
            pref2[i]=pref2[i-1]+yo2[i];
        }
        for(int i=m-1;i>0;i--){
            suf2[i-1]=suf2[i]+yo2[i];
        }

        for(int i=0;i<m-1;i++){
            if(suf2[i] && pref2[i] && pref2[i]==suf2[i])return true;
        }
        return false;
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