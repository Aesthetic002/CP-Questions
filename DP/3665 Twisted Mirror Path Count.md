## Problem Link [Here](https://leetcode.com/problems/twisted-mirror-path-count/description/)
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

  

    /*  0 1 1

        1 1 0  */

  

    long long MOD= 1000000007;

    int uniquePaths(vector<vector<int>>& grid) {

        int n=grid.size(),m=grid[0].size();

        if(grid[0][0])return 0;

        vector<vector<pair<int,int>>>yo(n,vector<pair<int,int>>(m,{0,0}));

        yo[0][0]={0,1};

        for(int i=0;i<n;i++){

            for(int j=0;j<m;j++){

                if(i==n-1 && j==m-1)return (yo[i][j].first%MOD + yo[i][j].second%MOD)%MOD;

                if(grid[i][j]){

                    if(i+1<n){

                        yo[i+1][j].second=yo[i][j].first%MOD;

                    }

                    if(j+1 <m){

                        yo[i][j+1].first=yo[i][j].second%MOD;

                    }

                }

                else{

                    if(i+1<n){

                        yo[i+1][j].second=(yo[i][j].first%MOD + yo[i][j].second%MOD)%MOD;

                    }

                    if(j+1 <m){

                        yo[i][j+1].first=(yo[i][j].first%MOD + yo[i][j].second%MOD)%MOD;

                    }

                }

            }

        }

  

        return yo[n-1][m-1].first + yo[n-1][m-1].second;

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