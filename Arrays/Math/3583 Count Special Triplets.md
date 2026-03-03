## Problem Link [Here](https://leetcode.com/problems/count-special-triplets/?envType=daily-question&envId=2025-12-09)

## Related Problems

## Topics [[Math]] [[Counting]] [[Maps]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int findd(vector<int>& arr, int a) {

    int s=0, e=arr.size()-1;

    int ans=-1;

    while(s<=e){

        int mid=s+(e-s)/2;

        if(arr[mid] < a){

            ans = mid;

            s = mid + 1;

        }else{

            e = mid - 1;

        }

    }

    return ans;

}

  

    int specialTriplets(vector<int>& nums) {

        map<int,vector<int>>mp;

        for(int i=0;i<nums.size();i++){

            mp[nums[i]].push_back(i);

        }

        long long MOD=1000000007;

        int cnt=0;

        for(auto &i:mp){

            if(i.first!=0 && mp.find(2*i.first)!=mp.end()){

                int n=mp[2*i.first].size();

                for(auto j:i.second){

                    int yo=findd(mp[2*i.first],j);

                    if(yo!=-1){

                        cnt=(cnt+(((yo+1)%MOD)*((n-yo-1))%MOD)%MOD)%MOD;

                    }

                }

            }

        }

        if(mp.find(0)!=mp.end()){

            int n=mp[0].size();

            cnt=(cnt+((((n)%MOD)*((n-1)%MOD) * ((n-2)%MOD)) /6))%MOD;

        }

        return cnt%MOD;

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