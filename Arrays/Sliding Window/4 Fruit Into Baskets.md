## Problem Link [Here](https://leetcode.com/problems/fruit-into-baskets/)


## My Approach

```cpp
class Solution {

public:

    int totalFruit(vector<int>& fruits) {

        pair<int,int> mp={-1,-1};

        pair<int,int> mp2={-1,-1};

        int s=0,e=0,maxi=0;

        while(e<fruits.size()){

            int temp=fruits[e];

            if(mp.first==-1){//Its a unique element

                mp.first=temp;

                mp.second=e;

                e++;

  

            }

  

            else if(mp2.first==-1 && temp!=mp.first){

                mp2.first=temp;

                mp2.second=e;

                e++;

            }

            else if(temp==mp.first || temp==mp2.first){

                if(temp==mp.first){

                    mp.second=e;

                }

                else{

                    mp2.second=e;

                }

                e++;

            }

            else{

                if(mp.second<mp2.second){

                    s=mp.second+1;

                    mp.first=temp;

                    mp.second=e;

                }

                else{

                    s=mp2.second+1;

                    mp2.first=temp;

                    mp2.second=e;                    

                }

  

                e++;

            }

  

            maxi=max(maxi,(e-s));

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