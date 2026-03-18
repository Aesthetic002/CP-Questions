## Problem Link [Here](https://leetcode.com/problems/longest-mountain-in-array/description/)
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]] [[Memoization]] [[Two Pointers]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    int longestMountain(vector<int>& arr) {
        int n=arr.size();
        vector<int>yo;
        for(int i=1;i<n-1;i++){
            if(arr[i-1]<arr[i] && arr[i]>arr[i+1])yo.push_back(i);
        }
        int maxi=0;
        for(auto i:yo){
            int j=i,k=i;
            while(j>0 && arr[j-1]<arr[j])j--;
            while(k<n-1 && arr[k+1]<arr[k])k++;
            maxi=max(maxi,k-j+1);
        }
        return maxi;
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