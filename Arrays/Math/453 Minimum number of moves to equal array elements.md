## Problem Link [Here](https://leetcode.com/problems/minimum-moves-to-equal-array-elements/description/)

### Related Problems

### Topics [[Math]]

### [Solutions]()


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int minMoves(vector<int>& nums) {

        int ans=0;int mini=INT_MAX;

        for(auto i:nums){

            mini=min(mini,i);

        }

  

        for(auto i:nums)ans+=i-mini;

  

        return ans;

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