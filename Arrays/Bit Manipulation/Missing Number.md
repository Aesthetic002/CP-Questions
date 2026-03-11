## Problem Link [Here](https://leetcode.com/problems/missing-number)

## Tags #Easy 
## Related Problems

## Topics [[Bit Manipulation]]

## Solutions


## My Approach

```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n=nums.size();
        int a=0,b=0;
        for(int i=0;i<=n;i++){
            a=(a)^(i);
            if(i<n)
            b=(b)^(nums[i]);
        }
        return (a)^(b);

    }
};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```