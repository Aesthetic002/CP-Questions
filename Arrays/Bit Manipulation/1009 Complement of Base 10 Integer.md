## Problem Link [Here](https://leetcode.com/problems/complement-of-base-10-integer/)
## Tags #Easy 
## Related Problems

## Topics [[Bit Manipulation]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    int bitwiseComplement(int n) {
        if(!n)return 1;
        string yo="";

        int ans=0;
        while(n){
            int rem=n&1;
            yo.push_back((!rem) +'0');
            n=n>>1;
        }

        reverse(yo.begin(),yo.end());


        for(auto i:yo){
            ans=(ans*2) + (i-'0');
        }
        return ans;
    }
};
```


## Approach 1

- [ ] **Works**

```cpp

class Solution {
public:
    int bitwiseComplement(int n) {
        unsigned long long int ans,mask,m;
        ans=0 , mask=0;
         m=n;
        if(n==0){
            return 1;
        }
        else{
        while(m!=0){
            mask=((mask<<1) | 1);
            m=(m>>1);
        }
       ans=((~n) & (mask));
        
        }
        
        return ans;
        
        }
    
};

```


## Approach 2

- [ ] **Works**

```cpp

```