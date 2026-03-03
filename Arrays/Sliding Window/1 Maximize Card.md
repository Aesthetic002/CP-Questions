## Problem Link   [Here](https://leetcode.com/submissions/detail/1780111258/)


## My Approach

```cpp
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        int n=cardPoints.size();
    int sum=0;int maxi;
        for(int i=0;i<k;i++){
            sum+=cardPoints[i];
        }
maxi=sum;

        for(int i=0;i<k;i++){
            int x=cardPoints[n-i-1]-cardPoints[k-i-1];
            sum+=x;
            maxi=max(maxi,sum);

        }
    // cout<<maxi;
    return maxi;

    }
};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```