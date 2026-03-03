## Problem Link [Here](https://leetcode.com/problems/number-of-perfect-pairs/description/)
## Tags 
## Related Problems

## Topics [[Two Pointers]] [[Sorting]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    long long perfectPairs(vector<int>& nums) {

        for(auto &i:nums){

            i=abs(i);

        }

        int n=nums.size();

        sort(nums.begin(),nums.end());

        long long cnt=0;

        int i=0,j=1;

        for(;i<n-1;i++){

            for(;j<n;j++){

                if(nums[j]> 2*nums[i]){cnt+=j-i-1;break;}

            }

            if(j==n)cnt+=j-i-1;

        }

        return cnt;

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