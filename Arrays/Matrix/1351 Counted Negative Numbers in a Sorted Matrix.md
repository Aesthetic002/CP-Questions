## Problem Link [Here](https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/?envType=daily-question&envId=2025-12-30)
## Tags 
## Related Problems

## Topics

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int countNegatives(vector<vector<int>>& grid) {

        int count=0;

        int up=0,left=0;

        int bot=grid.size()-1,right=grid[0].size()-1;

        while(bot>=up && right>=left){

            for(int j=right;j>=left;j--){

                if(grid[bot][j]>=0){

                    left=j+1;

                    break;

                }

                count++;

            }

            bot--;

            for(int i=bot;i>=up;i--){

                if(grid[i][right]>=0){

                    up=i+1;

                    break;

                }

                count++;

            }

            right--;

        }

  
  

        return count;

    }

};
```


## Chat GPT Approach 1

- [x] **Works**

```cpp
class Solution {
public:
    int countNegatives(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        int i = 0, j = n - 1;
        int count = 0;

        while (i < m && j >= 0) {
            if (grid[i][j] < 0) {
                // all elements below are negative
                count += (m - i);
                j--;
            } else {
                i++;
            }
        }
        return count;
    }
};

```


## Approach 2

- [ ] **Works**

```cpp

```