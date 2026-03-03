## Problem Link [Here](https://leetcode.com/problems/subarray-sum-equals-k/)


## My Approach

```cpp
class Solution {

public:

	int subarraySum(vector<int>& nums, int k) {
		unordered_map<int,int> mp;
		mp[0]=1;
		int pref=0,count=0;
		if(nums.size()==1){ 
			if(k==nums[0]) return 1;
			 else return 0;
			}
		for(int i=0;i<nums.size();i++){
			pref+=nums[i];
			int yo=pref-k;
			if(mp.find(yo)!=mp.end()) count+=mp[yo];
			if(mp.find(pref)!=mp.end()) mp[pref]++;
			else mp[pref]=1;
			}
		return count;
	}
	};
```


## Approach 1

```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        unordered_map<int,int> mp;
        mp[0] = 1;
        int pref = 0, count = 0;

        for (int x : nums) {
            pref += x;
            if (mp.count(pref - k))
                count += mp[pref - k];
            mp[pref]++;
        }

        return count;
    }
};

```


## Approach 2

```cpp

```