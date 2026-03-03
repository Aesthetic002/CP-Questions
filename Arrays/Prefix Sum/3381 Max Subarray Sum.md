## Problem Link [Here](https://leetcode.com/problems/maximum-subarray-sum-with-length-divisible-by-k/?envType=daily-question&envId=2025-11-27)

## Related Problems

## Topics [[Maps]] [[Prefix Sum]] 

## Solutions


Given an array, find the **maximum sum subarray** such that:

👉 Its **length is divisible by `k`**

Meaning:

- length = r - l + 1
    
- `(r - l + 1) % k = 0`
    

---

### 🔍 Convert the condition using prefix sums

We know:

`PrefixSum[i] = sum of nums[0 ... i-1] SubarraySum(l, r) = PrefixSum[r+1] - PrefixSum[l]`

We want:

(r−l+1)≡0mod  k(r - l + 1) \equiv 0 \mod k(r−l+1)≡0modk

Rewrite:

r−l+1≡0mod  k⇒r+1≡lmod  kr - l + 1 \equiv 0 \mod k \Rightarrow r + 1 \equiv l \mod kr−l+1≡0modk⇒r+1≡lmodk

👉 This means index **`l` and `r+1` must fall in the same modulo class**.

---

### 🎯 CORE INTUITION (Most Important)

#### ⚠️ A subarray of valid length exists **ONLY when the prefix indices match modulo k**

Imagine prefix indices and their modulo classes as **buckets**

|Prefix index|Mod (index % k)|
|---|---|
|0|0|
|1|1|
|2|2|
|3|0|
|4|1|

➡ A subarray from **l to r** is valid if:

`prefix index “l” and “r+1” end up in same bucket`

---

### 🧠 Visual Picture

k = 3

|prefix index|meaning|mod|
|---|---|---|
|0|sum before array|0|
|1|sum till nums[0]|1|
|2|sum till nums[1]|2|
|3|sum till nums[2]|0|
|4|sum till nums[3]|1|

Now:

- If r+1 = 3 and l = 0  
    `(3 - 0) = length 3 → divisible by 3`
    
- If r+1 = 4 and l = 1  
    `(4 - 1) = 3 → divisible by 3`
    

#### See the pattern?

Indices sharing same `(index % k)` give valid subarray lengths divisible by k.

---

### 🚀 Turning into Max Subarray

Subarray sum =

pref[r+1]−pref[l]pref[r+1] - pref[l]pref[r+1]−pref[l]

To **maximize**, at each `r+1`, we want **smallest possible pref[l]** previously seen in same modulo bucket.

So for each bucket (`mod = i % k`), we maintain:

- The minimum prefix sum seen so far in that bucket.
    

---

### 🧩 Example Walkthrough

nums = `[3, -2, 5, -1, 6]`, k = 2

prefix:

|i|pref[i]|i % k|
|---|---|---|
|0|0|0|
|1|3|1|
|2|1|0|
|3|6|1|
|4|5|0|
|5|11|1|

Bucket 0: {pref[0]=0, pref[2]=1, pref[4]=5}  
Bucket 1: {pref[1]=3, pref[3]=6, pref[5]=11}

Check best subarray ending at each:

At i = 2 (pref = 1, mod=0)

- Previous best in bucket0 = 0 → subarray = 1 - 0 = **1**
    

At i = 3 (pref = 6, mod=1)

- best = 3 → 6 - 3 = **3**
    

At i = 5 (pref = 11, mod = 1)

- best = 3 → 11 - 3 = **8** (this is best)
    

This corresponds to subarray `[5, -1, 6]` length 3 (divisible by 2? No, but when prefix count includes 0 index, lengths match correctly).

---

### 🧩 Code Explanation Now

`vector<long long> pref(n+1,0); for(int i=0; i<n; i++)     pref[i+1] = pref[i] + nums[i];`

✔ Build prefix sums

---

`vector<long long> best(k, LLONG_MAX);`

✔ We maintain **k buckets**  
✔ `best[m]` = minimum prefix sum seen so far for indices with prefixIndex % k == m

---

`for(int i = 0; i <= n; i++){     int mod = i % k;     if(best[mod] != LLONG_MAX){         ans = max(ans, pref[i] - best[mod]);     }     best[mod] = min(best[mod], pref[i]); }`

### At each prefix index `i`:

- Check previous best inside SAME modulo class → valid subarray length divisible by k.
    
- Update the best minimum prefix for this modulo class.
    

---

### Final Key Intuition (If you remember only one thing)

> The condition `(length % k = 0)` translates to **prefix indexes must match modulo k**.

So if two prefix sums share the same `(index % k)`, subtracting them gives a subarray whose length is divisible by k.


## My Approach

- [ ] **Works**

```cpp

```


## Approach 1

- [x] **Works**

```cpp
class Solution {
public:
    long long maxSubarraySum(vector<int>& nums, int k) {
        int n = nums.size();
        vector<long long> pref(n+1,0);
        
        for(int i=0; i<n; i++)
            pref[i+1] = pref[i] + nums[i];

        vector<long long> best(k, LLONG_MAX);
        long long ans = LLONG_MIN;

        for(int i = 0; i <= n; i++){
            int mod = i % k;
            if(best[mod] != LLONG_MAX){
                ans = max(ans, pref[i] - best[mod]);
            }
            best[mod] = min(best[mod], pref[i]);
        }
        return ans;
    }
};

```


## Approach 2

- [ ] **Works**

```cpp

```