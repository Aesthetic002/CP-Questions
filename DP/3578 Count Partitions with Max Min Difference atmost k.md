## Problem Link [Here](https://leetcode.com/problems/count-partitions-with-max-min-difference-at-most-k/description/?envType=daily-question&envId=2025-12-06)
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]] [[Memoization]] [[Queues]] [[Prefix Sum]] [[Sliding Window]]

## Solutions

### Approach 1: Sliding Window + Dynamic Programming

#### Intuition

The problem asks us to split the array nums into one or more **non-empty** contiguous subarrays such that, in every subarray, the difference between the **maximum** and **minimum** elements is at most k. We need to compute the total number of such valid partitioning schemes. Let n be the length of nums. We can enumerate each index i and calculate the number of valid partitions for the prefix nums[0⋯i]. Since the number of partitions at index i depends on the starting index j of the last subarray and the number of partitions for the prefix nums[0⋯j−1], dynamic programming is suitable.

Define dp[i+1] as the number of valid partitions for nums[0⋯i]. When i=0, the prefix is empty and is considered a valid base case, so we set dp[0]=1. Suppose the last subarray starts at index j. To compute dp[i], we need the number of partitions for the prefix nums[0⋯j−1], which is dp[j]. Since multiple starting positions may be valid, if the set of valid j values is j0​,j1​,…,jm−1​, we obtain the recurrence

dp[i+1]=∑s=0m−1​dp[js​].

Enumerating all such j values yields an O(n2) algorithm, so we need further optimization.

Next, consider the range of valid j. Fix the right endpoint i. As we extend the window leftward, the subarray grows and the max-min difference might exceed k. Hence the valid starting indices form a continuous interval [L,i], giving:

dp[i+1]=∑j=Li​dp[j].

We can compute this using prefix sums. Let

prefix[i+1]=∑j=0i​dp[j].

Then

dp[i+1]=prefix[i]−prefix[L−1].

The key step is to find the smallest valid L. If the max-min difference for nums[j⋯i] is within k, then all subarrays contained inside it also satisfy the condition. Thus we only need to maintain the smallest valid j. We can do this using the sliding window technique from problem 239, maintaining the max and min values within the window using an ordered set or a priority queue. When the difference exceeds k, we move the left boundary to restore validity. The final answer is dp[n].

The computation proceeds as follows:

- Initialize dp and prefix with dp[0]=1 and prefix[0]=1.
- For each index i, insert nums[i] into the ordered set. If the current max-min difference exceeds k, increment j and remove nums[j] until the window becomes valid again.
- Compute dp[i+1]=prefix[i]−prefix[j−1] and update prefix[i+1], applying the modulus as needed.
- After the loop finishes, return dp[n].
#### Complexity Analysis

Let n be the length of the array.

- Time complexiy: O(nlogn).
    
    Each element is inserted into and removed from an ordered multiset at most once. Each operation costs O(logn), and there are O(n) such operations.
    
- Space complexity: O(n).
    
    The ordered multiset can contain up to n elements, and the DP and prefix arrays each hold n+1 entries.
    

---

### [

](https://leetcode.com/problems/count-partitions-with-max-min-difference-at-most-k/editorial/?envType=daily-question&envId=2025-12-06#approach-2-monotonic-queue-optimization)

### Approach 2: Monotonic Queue Optimization

#### Intuition

When maintaining the sliding window, we can again refer to the ideas used in problem [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/). Instead of using an ordered set, we can further optimize the solution with monotonic queues. These queues maintain the maximum and minimum values in the current window, ensuring that the difference between them never exceeds k. Once this condition is met, the dynamic programming transitions follow the same structure described in the first approach.

#### Complexity Analysis

Let n be the length of the given array.

- Time complexity: O(n).
    
    Each index is pushed and popped from the monotonic queues at most once, so all queue operations together take linear time. The remaining work is also linear, giving a total of O(n).
    
- Space complexity: O(n).
    
    The monotonic queues can each hold up to n elements, and we store the DP and prefix arrays of size n+1, resulting in O(n) total space usage


## My Approach

- [ ] **Works**

```cpp
class Solution {

public:

    long long MOD = 1000000007;

    int countPartitions(vector<int>& nums, int k) {

        int n=nums.size();

        vector<int> mp(n);

        vector<int>dp(n+1,0);

        vector<int>pref(n+2,0);

        for(int i=0;i<n;i++){

            int mini=INT_MAX;

            int maxi=INT_MIN;  

            for(int j=i;j<n;j++){

                maxi=max(maxi,nums[j]);

                mini=min(mini,nums[j]);

                if(maxi - mini >k)break;

                mp[i]=j;

            }

        }

        dp[n]=1;

        pref[n]=1;

        for(int i=n-1;i>=0;i--){

            int lef = i+1;

            int rig= mp[i]+1;

  

            long long yo = ((pref[lef]-pref[rig+1])+MOD) % MOD;

            dp[i]=yo;

            pref[i]=((pref[i+1]%MOD)+(dp[i]%MOD)) %MOD;

        }

        return dp[0]%MOD;

        }

  
  

};
```


## Editorial Approach 1

- [x] **Works**

```cpp
class Solution {
public:
    int countPartitions(vector<int>& nums, int k) {
        int n = nums.size();
        long long mod = 1e9 + 7;
        vector<long long> dp(n + 1);
        vector<long long> prefix(n + 1);
        multiset<int> cnt;
        dp[0] = 1;
        prefix[0] = 1;
        for (int i = 0, j = 0; i < nums.size(); i++) {
            cnt.emplace(nums[i]);
            // adjust window
            while (j <= i && *cnt.rbegin() - *cnt.begin() > k) {
                cnt.erase(cnt.find(nums[j]));
                j++;
            }
            dp[i + 1] = (prefix[i] - (j > 0 ? prefix[j - 1] : 0) + mod) % mod;
            prefix[i + 1] = (prefix[i] + dp[i + 1]) % mod;
        }
        return dp[n];
    }
};
```


## Editorial Approach 2

- [x] **Works**

```cpp
class Solution {
public:
    int countPartitions(vector<int>& nums, int k) {
        int n = nums.size();
        long long mod = 1e9 + 7;
        vector<long long> dp(n + 1);
        vector<long long> prefix(n + 1);
        deque<int> minQ, maxQ;

        dp[0] = 1;
        prefix[0] = 1;
        for (int i = 0, j = 0; i < n; i++) {
            // maintain the maximum value queue
            while (!maxQ.empty() && nums[maxQ.back()] <= nums[i]) {
                maxQ.pop_back();
            }
            maxQ.push_back(i);
            // maintain the minimum value queue
            while (!minQ.empty() && nums[minQ.back()] >= nums[i]) {
                minQ.pop_back();
            }
            minQ.push_back(i);
            // adjust window
            while (!maxQ.empty() && !minQ.empty() &&
                   nums[maxQ.front()] - nums[minQ.front()] > k) {
                if (maxQ.front() == j) {
                    maxQ.pop_front();
                }
                if (minQ.front() == j) {
                    minQ.pop_front();
                }
                j++;
            }

            dp[i + 1] = (prefix[i] - (j > 0 ? prefix[j - 1] : 0) + mod) % mod;
            prefix[i + 1] = (prefix[i] + dp[i + 1]) % mod;
        }

        return dp[n];
    }
};
```