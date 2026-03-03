## Problem Link [Here](https://leetcode.com/problems/generate-parentheses/description/)


## My Approach

```cpp
class Solution {

public:

  

    void yo(vector<string>&ans,string output,int lcount,int rcount,int n){

        if(lcount==n){

            while(rcount!=n){

                output.push_back(')');

                rcount++;

            }

  

            ans.push_back(output);

            return;

        }

  

        output.push_back('(');

        yo(ans,output,lcount+1,rcount,n);

        output.pop_back();

        if(lcount>rcount){

            output.push_back(')');

            yo(ans,output,lcount,rcount+1,n);

        }

    }

    vector<string> generateParenthesis(int n) {

        vector<string>ans;

        string output;

        output.push_back('(');

        yo(ans,output,1,0,n);

        return ans;

    }

};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```