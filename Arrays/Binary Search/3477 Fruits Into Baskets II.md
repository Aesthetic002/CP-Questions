## Problem Link [Here](https://leetcode.com/problems/fruits-into-baskets-ii/)
## Tags #Easy 
## Related Problems

## Topics [[Binary Search]]

## Solutions


## My Approach (Brute Force)

- [ ] **Works**

```cpp
class Solution {

public:

    int numOfUnplacedFruits(vector<int>& fruits, vector<int>& baskets) {

        int n=fruits.size();

        int cnt=0;

        for(int i=0;i<n;i++){

            int j=0;

            for(;j<n;j++){

                if(baskets[j]>=fruits[i]){

                    baskets[j]=-1;

                    break;

                }

            }

            if(j==n)cnt++;

        }

        return cnt;

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