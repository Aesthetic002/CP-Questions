## Problem Link [Here](https://leetcode.com/problems/sliding-window-maximum/description/)
## Tags #Hard 
## Related Problems

## Topics [[Sliding Window]] [[Queues]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    vector<int> maxSlidingWindow(vector<int>& nums, int k) {

        int s=0,e=k-1;

        int n=nums.size();

        deque<int>st;

        vector<int>ans;

        for(int i=s;i<=e;i++){

            // if(st.em pty())st.push(nums[i]);

            while(!st.empty() && nums[st.back()]<nums[i])st.pop_back();

            st.push_back(i);

        }

        ans.push_back(nums[st.front()]);

        for(int i=k;i<n;i++){

            if(st.front()<=(i-k))st.pop_front();

            while(!st.empty() && nums[st.back()]<nums[i])st.pop_back();

            st.push_back(i);

            ans.push_back(nums[st.front()]);

        }

  

        return ans;

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