## Problem Link [Here](https://leetcode.com/problems/triangle/)

### Related Problems

### Topics

### [Solutions]()


## My Approach(Ganesh)

```cpp
class Solution {

public:

    int minimumTotal(vector<vector<int>>& triangle) {
        for(int i=triangle.size()-2;i>=0;i--){
            for(int j=0;j<triangle[i].size();j++){
                triangle[i][j]+=min(triangle[i+1][j],triangle[i+1][j+1]);
            }
        }
        return triangle[0][0];
    }
};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```