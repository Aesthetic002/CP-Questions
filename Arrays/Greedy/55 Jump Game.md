## Problem Link [Here](https://leetcode.com/problems/jump-game/description/)

### Related Problems

### Topics [[Greedy]] [[Tabulation]] [[Memoization]]

### Solutions 



## My Approach

```cpp
class Solution {

public:

    bool canJump(vector<int>& nums) {

        queue<int> q;

        int n=nums.size();

        for(int i=0;i<n;i++) if(!nums[i])q.push(i);

        if(q.size()==1 && q.front()==n-1) return true;

        int j=0;

        while(j < n){

            if(q.empty() || nums[j] >= (n-1 -j))return true;

            if(nums[j]==0 && q.front()==j)return false;

            int dist=q.front() - j;

            if(nums[j]>dist)q.pop();

            else j++;

        }

        return q.empty();

    }

};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```