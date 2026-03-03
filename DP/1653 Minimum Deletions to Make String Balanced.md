## Problem Link [Here](https://leetcode.com/problems/minimum-deletions-to-make-string-balanced/description/)
## Tags #Medium 
## Related Problems

## Topics [[Tabulation]] [[Memoization]] [[Stack]]

## Solutions

https://leetcode.com/problems/minimum-deletions-to-make-string-balanced/editorial/
## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int minimumDeletions(string s) {

        int n=s.size();

        int b=0;int yo=0;

        vector<int>cnt;  

        pair<int,int>maxi={INT_MIN,-1};

        for(int i=0;i<n;i++){

            if(s[i]=='b'){b++;yo--;}

            else yo++;

            cnt.push_back(b);

            if(yo>maxi.first){

                maxi={yo,i};

            }

        }

        if(n==b)return 0;

        int ans=INT_MAX;

            int op=cnt[maxi.second]+((n- (maxi.second+1))-(b-cnt[maxi.second]));

            ans=min(ans,op);

        return min(ans,n-b);

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