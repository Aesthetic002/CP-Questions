## Problem Link [Here](https://leetcode.com/problems/combination-sum/)

### Related Problems

### Topics


## My Approach

```cpp
class Solution {

public:

    vector<vector<int>>ans;

    void yo(vector<int>& candidates, vector<int>&temp,int &target,int sum,int index){

        if(sum==target){

            ans.push_back(temp);

            return;

        }

        if(sum>target || index >=candidates.size())return;

        yo(candidates,temp,target,sum,index+1);

        temp.push_back(candidates[index]);

        yo(candidates,temp,target,sum+candidates[index],index);

        temp.pop_back();

    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {

        vector<int>temp;

        yo(candidates,temp,target,0,0);

        return ans;

    }

};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```