## Problem Link [Here](https://leetcode.com/problems/3sum-closest/)
## Tags #Medium 
## Related Problems

## Topics [[Sorting]] [[Two Pointers]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int threeSumClosest(vector<int>& nums, int target) {

        sort(nums.begin(),nums.end());

        int n=nums.size();

        pair<int,int>mini={INT_MAX,INT_MAX};

        for(int i=0;i<n-2;i++){

            int j=i+1;

            int k=n-1;

  

            while(j<k){

                int d= (nums[i]+nums[j]+nums[k]);

                if(abs(d-target)<mini.first){

                    mini={abs(d-target),d};

                }

                if(d>target){

                    k--;

                }

                else if(d<target){

                    j++;

                }

                else return target;

            }

        }

        return mini.second;

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