## Problem Link [Here](https://leetcode.com/problems/maximum-number-of-subsequences-after-one-inserting/description/)
## Tags 
## Related Problems

## Topics

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    long long numOfSubsequences(string s) {

        long long lc=0,ct=0,lt=0,lct=0;

        vector<long long>lC,C;

        long long lcount=0,tcount=0;

  

        for(int i=0;i<s.length();i++){

            if(s[i]=='L'){

                lcount++;

            }

            else if(s[i]=='T'){

                lct+=lc;

            }

            else if(s[i]=='C'){

                lc+=lcount;
            }

            lC.push_back(lcount);

        }

        long long he=0;

        for(int i=s.length()-1;i>=0;i--){

            if(s[i]=='T'){

                tcount++;

            }

            else if(s[i]=='C'){

                ct+=tcount;

            }

            he=max(he,tcount*lC[i]);

        }

        return lct + max(lc,max(he,ct));

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