## Problem Link [Here](https://leetcode.com/problems/binary-subarrays-with-sum/)

### Related Problems
[[560 Subarray Sum]]

### Topics


## My Approach

This is the same code of Subarray Sum

```cpp
class Solution {

public:

    int subarraySum(vector<int>& nums, int k) {

        map<int,int> mp;

        mp[0]=1;

        int pref=0,count=0;

  

        if(nums.size()==1){

            if(k==nums[0])

                return 1;

            else return 0;

        }

        for(int i=0;i<nums.size();i++){

            pref+=nums[i];

  
  

            //Exclude

            int yo=pref-k;

            if(mp.find(yo)!=mp.end()){

                count+=mp[yo];

            }

  
  

            if(mp.find(pref)!=mp.end()){

                mp[pref]++;

            }

            else{

                mp[pref]=1;

            }

        }

  

        return count;

    }

};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```