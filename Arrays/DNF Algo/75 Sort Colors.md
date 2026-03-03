## Problem Link [Here](https://leetcode.com/problems/sort-colors/description/)
## Tags 
## Related Problems

## Topics

## Solutions


## My Approach

- [ ] **Works**

```cpp
class Solution {

public:

    void sortColors(vector<int>& nums) {

        int s=0,j=nums.size()-1;

        if(nums.size()==1)return;

        for(int i=0;i<=j;i++){

            if(nums[i]==2){

                while(j>=0 && nums[j]==2)j--;

                if(j>i){

                    swap(nums[j],nums[i]);

                    if(nums[i]==0){swap(nums[s],nums[i]);s++;}

                    j--;

                }

            }

            else if(nums[i]==0){

                swap(nums[s],nums[i]);

                s++;

            }

        }

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