## Problem Link [Here](https://leetcode.com/problems/minimum-moves-to-balance-circular-array/)
## Tags #Medium 
## Related Problems

## Topics

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    long long minMoves(vector<int>& b) {

        int n=b.size();

        int j=-1;

        long long sum=0;

        for(int i=0;i<n;i++){

            if(b[i]<0){

                j=i;

            }

            sum+=(long long) b[i];

        }

        if(sum<0)return -1;

        if(j==-1)return 0;

        long long ans=0;

        int val=abs(b[j]);

        int l=0;

        if(j==0)

            l=(n-1);

            else l=(j-1);

        int r=(j+1) %n;

        for(int k=1;k<=((n-1)/2);k++){

            int yo=b[l] + b[r];

            if(yo>=val){

                return ans=ans+ ((long long)val * (long long)k);

            }

            ans=ans+ ((long long)yo * (long long)k);

            r=(r+1) %n;

            if(l==0)

            l=(n-1);

            else l=(l-1);

            val=val-yo;

        }

        if(n%2==0){

        // r=(r+1) %n;

        ans=ans+ ((long long)val * (long long)(((n-1)/2)+1));

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