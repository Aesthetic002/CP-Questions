## Problem Link [Here](https://leetcode.com/problems/construct-uniform-parity-array-ii/description/)
## Tags #Medium
## Related Problems

## Topics [[Maps]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    bool uniformArray(vector<int>& nums1) {
        set<int>odd,even;
        int n=nums1.size();
        int cnt=0;
        for(auto i:nums1){
            if(i%2==0)even.insert(i);
            else odd.insert(i);
        }
        if(odd.size()==0 || even.size()==0)return true;
        //all odd
        bool e=true;
        for(auto i:even){
            if(i-*odd.begin()<1){e=false;break;}
        }
        if(e)return true;
        return false;
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