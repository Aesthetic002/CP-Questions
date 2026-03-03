## Problem Link [Here](https://leetcode.com/problems/smallest-missing-non-negative-integer-after-operations/)
## Tags #Medium 
## Related Problems

## Topics [[Greedy]] [[Math]] 

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int findSmallestInteger(vector<int>& nums, int value) {

        map<int,int>mp;  // 1 4 0 6 6 1    0  1 1  4  6 6           0 1 2 3 4 5

        int n=nums.size();

        vector<int>yo(n,1);

        for(auto i:nums){

            int he=(i%value);

            if(he<0)he+=value;

            if(he<n && yo[he])yo[he]=0;

            else mp[he]++;

        }

        for(auto &i:mp){

            int t=i.first;

            while(i.second--){

                while(t<n  && (!yo[t]) ){

                    t+=value;

                }

                if(t<n){

                    yo[t]=0;

                }

  

            }

        }

        for(int i=0;i<n;i++){

            if(yo[i])return i;

        }

        return n;

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