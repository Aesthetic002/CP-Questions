## Problem Link [Here](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-using-strategy/?envType=daily-question&envId=2025-12-18)
## Tags 
## Related Problems

## Topics

## Solutions

### [Editorial](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-using-strategy/editorial/?envType=daily-question&envId=2025-12-18#approach-prefix-sum)

### Approach: Prefix Sum

#### Intuition

Let n be the length of the array prices. Assuming that the k consecutive elements we choose lie within the interval `[i−k+1,i] `(where i≥k−1), the profit consists of three parts:

1. The sum of all strategy`[j]`×prices`[j]` in the interval `[0,i−k]`
    
2. The sum of all prices`[j] `in the interval `[i−2k​+1,i]`
    
3. The sum of all strategy`[j]`×prices`[j]` in the interval `[i+1,n−1]`
    

We use the array profitSum to keep track of the prefix sums of strategy`[j]`×prices`[j]`, and the array priceSum to keep track of the prefix sums of prices`[j]`. We iterate through i in order and use the prefix sum arrays to calculate the three parts of the profit, returning the maximum profit obtained.

#### Complexity Analysis

Let n be the length of prices.

- Time complexity: O(n).
    
- Space complexity: O(n).
## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    long long maxProfit(vector<int>& prices, vector<int>& strategy, int k) {

        int n = prices.size();

        long long maxi = 0;

        int s = 0, e = k - 1;

        long long sum1 = 0;

        long long y = 0;

        for (int i = 0; i < k/2; i++) {

            y+=strategy[i]*prices[i];

        }

        for (int i = k/2; i < k; i++) {

            sum1+=prices[i];

            y+=strategy[i]*prices[i];

        }

        for(int i=k;i<n;i++){

            sum1+=strategy[i]*prices[i];

            y+=strategy[i]*prices[i];

        }

        maxi = max(y,sum1);

        while (e < n - 1) {

            sum1 -= prices[s+(k/2)];

            sum1 += prices[s]*strategy[s];

            sum1-=prices[e+1]*strategy[e+1];

            sum1+=prices[e+1];

            s++,e++;

            maxi=max(maxi,sum1);

        }

        return maxi;

    }

};
```


## Editorial Approach 1

- [ ] **Works**

```cpp
class Solution {
public:
    long long maxProfit(vector<int>& prices, vector<int>& strategy, int k) {
        int n = prices.size();
        vector<long long> profitSum(n + 1);
        vector<long long> priceSum(n + 1);
        for (int i = 0; i < n; i++) {
            profitSum[i + 1] = profitSum[i] + prices[i] * strategy[i];
            priceSum[i + 1] = priceSum[i] + prices[i];
        }
        long long res = profitSum[n];
        for (int i = k - 1; i < n; i++) {
            long long leftProfit = profitSum[i - k + 1];
            long long rightProfit = profitSum[n] - profitSum[i + 1];
            long long changeProfit = priceSum[i + 1] - priceSum[i - k / 2 + 1];
            res = max(res, leftProfit + changeProfit + rightProfit);
        }
        return res;
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```
