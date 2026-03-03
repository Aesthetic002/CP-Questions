## Problem Link [Here](https://leetcode.com/problems/maximum-capacity-within-budget/description/)
## Tags 
## Related Problems

## Topics [[Prefix Sum]] [[Binary Search]]

## Solutions

### Problem Summary

You are given:

- `costs[i]` → purchase cost of the _i-th_ machine
    
- `capacity[i]` → performance capacity of the _i-th_ machine
    
- An integer `budget`
    

---

###  Rules

- You may select **at most two distinct machines**
    
- Total cost must be **strictly less than `budget`**
    
- Objective: **maximize total capacity**
    

---

###  Approach Overview

We handle the problem by considering **two cases**:

1. Selecting **one machine**
    
2. Selecting **two machines**
    

Checking all pairs directly leads to **O(n²)** time, which is inefficient.

We optimize using:

- Sorting
    
- Prefix maximum array
    
- Binary search
    

Final time complexity becomes **O(n log n)**.

---

###  Step 1: Combine Cost and Capacity

Store machines as pairs:

`(cost, capacity)`

This allows easy sorting and access.

---

###  Step 2: Sort Machines by Cost

Sort all machines in **ascending order of cost**.

Why sorting?

- Enables binary search for affordable machines
    
- Maintains increasing cost order
    

---

###  Step 3: Prefix Maximum Capacity Array

Create an array `bestCap[]` such that:

`bestCap[i] = max capacity from index 0 to i`

Purpose:

- Quickly obtain the highest capacity machine within a cost limit
    

---

###  Step 4: Case 1 – Selecting One Machine

For every machine:

- If `cost < budget`
    
- Update the answer with its capacity
    

---

###  Step 5: Case 2 – Selecting Two Machines

For each machine `i` (considered as the second machine):

1. Compute remaining budget:
    

`remaining = budget - cost[i] - 1`

(`-1` ensures total cost is strictly less than budget)

2. Use **binary search** to find the largest index `j < i` such that:
    

`cost[j] ≤ remaining`

3. Compute total capacity:
    

`totalCapacity = capacity[i] + bestCap[j]`

4. Update maximum answer
    

---

###  Final Result

Return the **maximum total capacity** obtained by:

- Selecting one machine
    
- Selecting two machines
    

---

## My Approach

- [ ] **Works**

```cpp

```


## Approach 1

- [ ] **Works**

```cpp
class Solution {
public:
    int maxCapacity(vector<int>& costs, vector<int>& capacity, int budget) {
        int n = costs.size();
        vector<pair<int,int>> machines;

        // Step 1: Combine cost and capacity
        for (int i = 0; i < n; i++) {
            machines.push_back({costs[i], capacity[i]});
        }

        // Step 2: Sort by cost
        sort(machines.begin(), machines.end());

        // Step 3: Prefix maximum capacity
        vector<int> bestCap(n);
        bestCap[0] = machines[0].second;
        for (int i = 1; i < n; i++) {
            bestCap[i] = max(bestCap[i - 1], machines[i].second);
        }

        int ans = 0;

        // Step 4: One machine case
        for (int i = 0; i < n; i++) {
            if (machines[i].first < budget) {
                ans = max(ans, machines[i].second);
            }
        }

        // Step 5: Two machine case
        for (int i = 1; i < n; i++) {
            int remaining = budget - machines[i].first - 1;
            if (remaining < 0) continue;

            int l = 0, r = i - 1, idx = -1;
            while (l <= r) {
                int mid = (l + r) / 2;
                if (machines[mid].first <= remaining) {
                    idx = mid;
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }

            if (idx != -1) {
                ans = max(ans, machines[i].second + bestCap[idx]);
            }
        }

        return ans;
    }
};

```


## Approach 2

- [ ] **Works**

```cpp

```