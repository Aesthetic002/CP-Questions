## Problem Link [Here](https://leetcode.com/problems/matrix-similarity-after-cyclic-shifts/description/)
## Tags #Easy 
## Related Problems

## Topics

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    bool areSimilar(vector<vector<int>>& mat, int k) {
        int n=mat.size(),m=mat[0].size();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(j%2==0) {if(mat[i][(k+j)%m]!=mat[i][j])return false;}
                else if(mat[i][(m-(k%m)+j)%m]!=mat[i][j])return false;
            }
        }
        return true;
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