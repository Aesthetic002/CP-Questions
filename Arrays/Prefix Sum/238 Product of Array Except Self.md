## Problem Link [Here](https://leetcode.com/problems/product-of-array-except-self/description/)
## Tags #Medium 
## Related Problems

## Topics [[Prefix Sum]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n=nums.size();
        vector<int>pref(n);
        vector<int>suf(n);
        int p1=1,p2=1;
        for(int i=0;i<n;i++){
            pref[i]=p1;
            p1*=nums[i];
        }
        for(int i=n-1;i>=0;i--){
            suf[i]=p2;
            p2*=nums[i];
        }

        for(int i=0;i<n;i++){
            nums[i]=pref[i]*suf[i];
        }
        return nums;

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