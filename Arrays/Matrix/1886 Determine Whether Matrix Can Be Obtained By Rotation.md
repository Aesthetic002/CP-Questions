## Problem Link [Here](https://leetcode.com/problems/determine-whether-matrix-can-be-obtained-by-rotation/description/?envType=daily-question&envId=2026-03-22)
## Tags #Easy 
## Related Problems

## Topics

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    vector<vector<int>> yo(vector<vector<int>>& mat){
        int n=mat.size();
        vector<vector<int>>ans(n,vector<int>(n));

        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                ans[j][n-i-1]=mat[i][j];
            }
        }
        return ans;
    }
    bool findRotation(vector<vector<int>>& mat, vector<vector<int>>& target) {
        
        if(mat==target)return true;
        for(int i=0;i<3;i++){
            mat=yo(mat);
            if(mat==target)return true;
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