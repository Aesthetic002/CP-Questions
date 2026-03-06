## Problem Link [Here](https://leetcode.com/problems/count-binary-substrings/description/?envType=daily-question&envId=2026-02-19)
## Tags #Easy
## Related Problems

## Topics [[Two Pointers]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int countBinarySubstrings(string s) {

        vector<int>yo;

        char in=s[0];

        int cnt=0;

        for(int i=0;i<s.size();i++){

            if(s[i]==in){

                cnt++;

            }

            if(s[i]!=in){

                yo.push_back(cnt);

                in=s[i];

                cnt=1;

            }

            if(i==s.size()-1){

                yo.push_back(cnt);

            }

        }

        // for(auto i:yo)cout<<i<<" ";

        int ans=0,n=yo.size();

        for(int i=0;i<n-1;i++){

            ans+=min(yo[i],yo[i+1]);

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