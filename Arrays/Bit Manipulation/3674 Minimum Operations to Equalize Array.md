## Problem Link [Here](https://leetcode.com/problems/minimum-operations-to-equalize-array/)
## Tags #Easy 
## Related Problems

## Topics [[Bit Manipulation]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    int minOperations(vector<int>& nums) {
        for(int i=1;i<nums.size();i++){
            if(nums[i]!=nums[i-1])return 1;
        }
        return 0;
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