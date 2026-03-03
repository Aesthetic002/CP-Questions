## Problem Link [Here]()

### Related Problems

### Topics

### [Solutions]()


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int maxSubArray(vector<int>& nums) {

        int maxi=INT_MIN,sum=0;

        for(auto i:nums){

            if(sum<0 && i>sum){

                sum=i;

            }

            else{

                sum+=i;

            }

            maxi=max(maxi,sum);

        }

  

        return maxi;

    }

};
```


## Approach 1

- [x] **Works**

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxSum = nums[0];
        int currSum = nums[0];

        for(int i = 1; i < nums.size(); i++) {
            currSum = max(nums[i], currSum + nums[i]);
            maxSum = max(maxSum, currSum);
        }
        return maxSum;
    }
};

```


## Approach 2

- [ ] **Works**

```cpp

```