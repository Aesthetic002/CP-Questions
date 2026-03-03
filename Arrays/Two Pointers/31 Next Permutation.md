## Problem Link [Here](https://leetcode.com/problems/next-permutation/description/)
## Tags #Medium 
## Related Problems

## Topics [[Two Pointers]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    void nextPermutation(vector<int>& nums) {

        int n=nums.size();

        for(int i=n-2;i>=0;i--){

            int mini=-1;

            for(int j=i+1;j<n;j++){

                if(nums[j]>nums[i]){

                    if(mini==-1 || nums[j]<nums[mini])

                    mini=j;

                }

            }

            if(mini!=-1){

                swap(nums[i],nums[mini]);

                reverse(nums.begin()+i+1,nums.end());

                return;

            }

        }

        reverse(nums.begin(),nums.end());

        return;

    }

};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {

public:

    void nextPermutation(vector<int>& nums) {

        int i,j,n=nums.size();

        for(i=n-2;i>=0 ;i--){

            if(i>=0 && nums[i]<nums[i+1]){

                break;

            }

        }

        if(i==-1){

            reverse(nums.begin(),nums.end());

            return ;

        }

  

        for(j=n-1;j>0 ;j--){

            if(nums[j]>nums[i]){

                break;

            }

        }

  

        swap(nums[i],nums[j]);

        reverse(nums.begin()+i+1,nums.end());

        return;

    }

};
```


## Approach 2

- [ ] **Works**

```cpp

```