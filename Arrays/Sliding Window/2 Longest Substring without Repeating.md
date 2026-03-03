## Problem Link [Here](https://leetcode.com/submissions/detail/1780181593/)


## My Approach

```cpp

class Solution {

public:

    int yo(string s,int st,int e,char temp){

        for(int i=st;i<=e;i++){

            if(s[i]==temp){

                return i;

            }

        }

  

        return -1;

    }

    int lengthOfLongestSubstring(string s) {

        int maxi=0;

        int st=0,e=0;

        int index;

        if(s.size()==0){

            return 0;

        }

        else if(s.size()==1){

            return 1;

        }

  

       for(int i=1;i<s.size();i++){

            char temp=s[i];

            if((index=yo(s,st,e,temp))!=-1){

                st=index+1;

                e++;

  

            }

            else{

                e++;

            }cout<<index<<" ";

            maxi=max(maxi,(e-st+1));

            // cout<<st<<" "<<e<<" "<<maxi<<" "<<i<<endl;

        }

        return maxi;

    }

};
```


## Approach 1

```cpp
class Solution {

public:

  

    int lengthOfLongestSubstring(string s) {

        map<char,int> mp;

        int maxi=0;

        int st=0,e=0;

        int index;

        if(s.size()==0){

            return 0;

        }

        else if(s.size()==1){

            return 1;

        }

  

       for(int i=0;i<s.size();i++){

            char temp=s[i];

            if(mp.find(temp)==mp.end() || mp[temp]<st){

                e=i;

                mp[temp]=e;

  

            }

            else{

                st=mp[temp]+1;

                mp[temp]=i;

            }

            maxi=max(maxi,(e-st+1));

            // cout<<st<<" "<<e<<" "<<maxi<<" "<<i<<endl;

        }

        return maxi;

    }

};
```


## Approach 2

```cpp

```