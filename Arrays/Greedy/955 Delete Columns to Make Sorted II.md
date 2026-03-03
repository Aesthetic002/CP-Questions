## Problem Link [Here](https://leetcode.com/problems/delete-columns-to-make-sorted-ii/description/)
## Tags #Medium 
## Related Problems

## Topics

## Solutions

#### Approach 1: Greedy

**Intuition**

Instead of thinking about column deletions, let's think about which columns we will keep in the final answer.

If the first column isn't lexicographically sorted, we have to delete it.

Otherwise, we will argue that we can keep this first column without consequence. There are two cases:

- If we don't keep the first column, then the final rows of the answer all have to be sorted.
    
- If we do keep the first column, then the final rows of the answer (minus the first column) only have to be sorted if they share the same first letter (coming from the first column).
    
    The above statement is hard to digest, so let's use an example:
    
    Say we have `A = ["axx","ayy","baa","bbb","bcc"]`. When we keep the first column, the final rows are `R = ["xx","yy","aa","bb","cc"]`, and instead of the requirement that these all have to be sorted (ie. `R[0] <= R[1] <= R[2] <= R[3] <= R[4]`), we have a weaker requirement that they only have to be sorted if they share the same first letter of the first column, (ie. `R[0] <= R[1] and R[2] <= R[3] <= R[4]`).
    

Now, we applied this argument only for the first column, but it actually works for every column we could consider taking. If we can't take a column, we have to delete it. Otherwise, we take it because it can only make adding subsequent columns easier.

**Algorithm**

All our effort has led us to a simple algorithmic idea.

Start with no columns kept. For each column, if we could keep it and have a valid answer, keep it - otherwise delete it.

**Complexity Analysis**

- Time Complexity: O(NW2), where N is the length of `A`, and W is the length of `A[i]`.
    
- Space Complexity: O(NW).


#### Approach 2: Greedy with Optimizations

**Explanation**

It is also possible to implement the solution in _Approach 1_ without using as much time and space.

The key idea is that we will record the "cuts" that each column makes. In our first example from _Approach 1_ with `A = ["axx","ayy","baa","bbb","bcc"]` (and `R` defined as in Approach 1), the first column cuts our condition from `R[0] <= R[1] <= R[2] <= R[3] <= R[4]` to `R[0] <= R[1]` and `R[2] <= R[3] <= R[4]`. That is, the boundary `"a" == column[1] != column[2] == "b"` has 'cut' one of the conditions for `R` out.

At a high level, our algorithm depends on evaluating whether adding a new column will keep all the rows sorted. By maintaining information about these cuts, we only need to compare characters in the newest column.

**Complexity Analysis**

- Time Complexity: O(NW), where N is the length of `A`, and W is the length of `A[i]`.
    
- Space Complexity: O(N) in additional space complexity. (In Python, `zip(*A)` uses O(NW) space.)
## My Approach

- [ ] **Works**

```cpp
class Solution {

public:

    int minDeletionSize(vector<string>& strs) {

        int n=strs.size(),m=strs[0].size();

        int ans=0;

        vector<int>sat(n,-1);

        for(int j=0;j<m;){

            bool yo=true;

            int i=0;

            int index=0;

            int del=-1;

            do{

                if(i==n-1){ i=(i+1)%n;continue;}

                if(strs[i][j]<strs[i+1][j]){

                sat[i]=j;

                i=(i+1)%n;

                continue;}

                if(sat[i]==-1 || (sat[i]+1==j && del!=-1)){

                while(j<m && strs[i][j]>strs[i+1][j]){

                    ans++;

                    del=j;

                    j++;

                    yo=true;

                    index=i;

                    sat[i]=-1;

                }

                if(j>=m)return ans;

            }

                i=(i+1)%n;

            }while(i!=index);

            if(yo){

                return ans;

            }

            else j++;

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
    int minDeletionSize(vector<string>& A) {
        int N = A.size();
        int W = A[0].size();
        int ans = 0;

        // cur: prefixes formed so far for each row
        vector<string> cur(N, "");

        for (int j = 0; j < W; ++j) {
            // cur2 = cur + current column
            vector<string> cur2 = cur;
            for (int i = 0; i < N; ++i) {
                cur2[i].push_back(A[i][j]);
            }

            if (isSorted(cur2)) {
                cur = cur2;
            } else {
                ans++;
            }
        }
        return ans;
    }

    bool isSorted(const vector<string>& A) {
        for (int i = 0; i + 1 < A.size(); ++i) {
            if (A[i] > A[i + 1])
                return false;
        }
        return true;
    }
};

```


## Approach 2

- [ ] **Works**

```cpp

```