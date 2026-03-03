## Problem Link [Here](https://leetcode.com/problems/unique-paths/submissions/1840457438/)

## Related Problems

## Topics [[Tabulation]] [[Math]] [[GridDP]]

## Solutions

### Tabulation
There are 2 ways to enter a cell..the total number of ways would be  sum of the both.
### Math
From (0,0) to (m-1,n-1) there are `n horizontal distances` and `m vertical distances`.
So the question becomes ..arrange n H's and m V's ..that is (n+m)C(min(n,m))

## My Approach-(Tabulation)

- [x] **Works**

```cpp
class Solution {

public:

    int uniquePaths(int m, int n) {

        vector<vector<int>>yo(m,vector<int>(n,0));

  

        for(int i=0;i<m;i++){

            for(int j=0;j<n;j++){

                if(i==0 && j==0){

                    yo[0][0]=1;

                    continue;

                }

                if(i-1>=0){

                    yo[i][j]+=yo[i-1][j];

                }

                if(j-1>=0){

                    yo[i][j]+=yo[i][j-1];

                }

            }

        }

  

        return yo[m-1][n-1];

    }

};
```


## My Approach (Mathematics)

- [x] **Works**

```cpp
class Solution {

public:

    int uniquePaths(int m, int n) {

        int N=n+m-2;long long a=1;int r=min(n-1,m-1);

        for(int i=1;i<=r;i++){

            a=a * (N-r+i)/i;

        }

  

        return (int)a;

    }

};
```


## Approach 2

- [ ] **Works**

```cpp

```