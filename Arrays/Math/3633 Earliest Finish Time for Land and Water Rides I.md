## Problem Link [Here](https://leetcode.com/problems/earliest-finish-time-for-land-and-water-rides-i/description/)
## Tags #Easy 
## Related Problems

## Topics [[Math]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {

public:

    int earliestFinishTime(vector<int>& lt, vector<int>& ld, vector<int>& wt, vector<int>& wd) {

        int mini=INT_MAX;

        for(int i=0;i<lt.size();i++){

            for(int j=0;j<wt.size();j++){

                if(lt[i]<wt[j]){

                    int c=lt[i]+ld[i];

                    if(c>=wt[j]){

                        mini=min(mini,c+wd[j]);

                    }

                    else{

                        mini=min(mini,wt[j]+wd[j]);

                    }

                }

                else{

                    int c=wt[j]+wd[j];

                    if(c>=lt[i]){

                        mini=min(mini,c+ld[i]);

                    }

                    else{

                        mini=min(mini,lt[i]+ld[i]);

                    }

                }

            }

        }

        return mini;

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