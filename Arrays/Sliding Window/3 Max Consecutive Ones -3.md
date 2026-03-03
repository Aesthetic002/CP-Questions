## Problem Link [Here](https://leetcode.com/submissions/detail/1781067697/)


## My Approach

```cpp
class Solution {

public:

    int longestOnes(vector<int>& nums, int k) {

        //keep windows sliding until atmost k zeroes

        int s=0,e=0,maxi=0;

        int Zcount=0;

        while(e<nums.size()){

            if(nums[e]==0 && Zcount>=k){

                Zcount++;

                while(Zcount>k){

                    if(nums[s]==0){

                        Zcount--;

                    }

                    s++;

                }

                e++;

            }

            else if((nums[e]==0)&&(Zcount<k)){

                Zcount++;

                e++;

            }

            else{

                e++;

            }

            maxi=max(maxi,e-s);

            cout<<s<<" "<<e<<" "<<maxi<<" "<<endl;

        }

  
  

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