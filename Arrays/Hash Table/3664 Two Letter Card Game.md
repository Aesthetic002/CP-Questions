## Problem Link [Here](https://leetcode.com/problems/two-letter-card-game/)
## Tags #Medium 
## Related Problems

## Topics [[Maps]] [[Counting]] [[Enumeration]]

## Solutions


## My Approach

- [ ] **Works**

```cpp
class Solution {

public:

    int score(vector<string>& cards, char x) {

        map<string,int>mp;

        for(auto i:cards){

            if(i[0]==x || i[1]==x ){

                sort(i.begin(),i.end());

                mp[i]++;

            }

        }

        int ans=0;

        while(mp.size()!=1 && mp.size()!=0){

                auto hi=mp.end();

                if(mp.size()%2!=0){

                --hi;

                }

                vector<string>del;

            for(auto i=mp.begin();i!=hi;++i){

                i->second--;

                ans++;

                if(!i->second){

                    del.push_back(i->first);

                }

            }

                for(auto i:del){

                    mp.erase(i);

                }

        }

        return ans/2;

  

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