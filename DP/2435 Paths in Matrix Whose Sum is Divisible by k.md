## Problem Link [Here](https://leetcode.com/problems/paths-in-matrix-whose-sum-is-divisible-by-k/description/?envType=daily-question&envId=2025-11-26)

## Related Problems

## Tags #Hard 

## Topics [[Memoization]] [[Tabulation]]

## Solutions

### Memoization

#### 🧠 Intuition Behind Memoization (Top-Down DP)

##### Problem in simple words

You are moving from the top-left to the bottom-right of a grid.  
At every move, you can go either **right or down**.  
You want to count the number of paths such that the **sum of all visited cells is divisible by k**.

---

#### 1. What does memoization mean here?

Instead of recomputing the same paths again and again, we **remember results of smaller problems**.

We break the big problem into smaller ones like:

> "From this cell, how many valid paths exist till the destination?"

---

#### 2. The core question we ask recursively

At any position (i, j), we ask:

> If my current sum modulo k is `rem`, how many ways can I reach the bottom-right from here?

This becomes our function:

`dfs(i, j, rem)`

Meaning:

- i, j → current cell
    
- rem → remainder of the path sum so far when divided by k
    
- return → number of valid paths from here
    

---

#### 3. Why do we track remainder instead of full sum?

Because the problem only cares if:

`(sum % k == 0)`

So the exact sum doesn't matter, only the remainder does.

This reduces infinite possibilities into only `k` states:

`0, 1, 2, ..., k-1`

---

#### 4. Base Case (Stopping Condition)

When we reach the last cell `(n-1, m-1)`:

We add its value to the current sum and check:

`if remainder == 0     this path is valid (count = 1) else     invalid (count = 0)`

---

#### 5. Recursive Thinking

From cell (i, j), you have only two choices:

1. Go Down → (i+1, j)
    
2. Go Right → (i, j+1)
    

So:

`dfs(i, j, rem) =     dfs(i+1, j, new_rem) +     dfs(i, j+1, new_rem)`

Where:

`new_rem = (rem + grid[i][j]) % k`

---

#### 6. Why memoization is powerful

Without memoization:

- Same states (i, j, rem) are calculated many times
    
- Time becomes exponential
    

So we store results in:

`dp[i][j][rem]`

Which means:

> Number of valid paths from (i,j) when the current remainder is rem.

If we encounter the same state again:  
we just return the stored value instead of recalculating.

---

#### 📌 Complete Mental Model (Note-Friendly)

You can write this in your notes:

---

##### Recursive State Definition:

`dfs(i, j, r) = number of paths from cell (i,j) to bottom-right                such that current path sum % k = r`

---

##### Transition:

`new_r = (r + grid[i][j]) % k  dfs(i, j, r) =     dfs(i+1, j, new_r) +     dfs(i, j+1, new_r)`

---

##### Base Case:

`If (i, j) is last cell: return 1 if new_r == 0 else 0`

---

##### Memoization:

Store results in:

`dp[i][j][r]`

So each state is computed only once.

---

#### 🧠 Intuition Summary (short)

- Every recursive call asks:  
    "From here, how many valid paths exist?"
    
- Only three things define a state:
    
    - row index
        
    - column index
        
    - remainder modulo k
        
- We store results to avoid recomputation.
    
- The same (position, remainder) always gives the same answer.
    

---

#### Real-world Analogy

Think of each cell as a checkpoint.  
You reach it with different balances (remainders).  
If you reach with the same balance again, the future outcomes will be identical — so reuse the result.

---

#### 🎯 Why this guarantees correctness

Because:

- All paths are explored
    
- No path is double-counted
    
- No valid path is missed
    
- Recursive structure mirrors real movement

###### This was my older graph approach..The memoization part comes where i store the path and use it afterwards.

```cpp
class Solution {

public:

    int count=0;

    void dfs(vector<vector<int>>& grid,vector<vector<int>>&vis, int &k,int &sum,int i,int j){

        int m=grid.size(),n=grid[0].size();

        if(i== m-1 && j==n-1){

            if((sum+grid[i][j])%k==0)count++;

            return;

        }

  

        vis[i][j]=1;

        sum+=grid[i][j];

        int a=i+1,b=j;

        if(a<m && b<n && vis[a][b]==0){

            dfs(grid,vis,k,sum,a,b);

        }

        a--,b++;

        if(a<m && b<n && vis[a][b]==0){

            dfs(grid,vis,k,sum,a,b);

        }

        sum-=grid[i][j];

        vis[i][j]=0;

  
  

    }

    int numberOfPaths(vector<vector<int>>& grid, int k) {

        int m=grid.size(),n=grid[0].size();

        vector<vector<int>>vis(m,vector<int>(n,0));

        int sum=0;

        dfs(grid,vis,k,sum,0,0);

        return count;

  

    }

};
```

Here vis is not actually required..Its only required when there is case of revisiting the same node at the path.Foe Example if there were four directions allowed then vis would be helpful.Now since the indices are strictly increasing its not needed.

### Tabulation
#### 🧠 Intuition Behind Tabulation (Bottom-Up DP)

##### Problem Overview

You move from the top-left cell to the bottom-right cell of a grid.  
You can move only:

- ➡️ Right
    
- ⬇️ Down
    

You must count paths where:

`(total sum of visited cells) % k == 0`

---

#### 1. What is Tabulation?

Tabulation means:

> Solve smaller cases first and store their results in a table, then build larger answers from them.

Instead of recursion, we **fill the answer step-by-step** from the start cell.

---

#### 2. The Core Question Each Cell Asks

At every cell, we ask:

> "How many ways can I reach here with each possible remainder?"

So each cell stores multiple answers.

---

#### 3. State Definition

We define a 3D table:

`dp[i][j][r]`

Meaning:

> Number of ways to reach cell (i, j) such that  
> the sum of the path modulo k = r

Where:

- i = row
    
- j = column
    
- r = remainder (0 to k-1)
    

---

#### 4. Why we store only remainder?

We only care about:

`sum % k`

So instead of infinite possible sums, we only track:

`0, 1, 2, ..., k-1`

This keeps the problem small and efficient.

---

#### 5. How Values Flow (Transition Logic)

To reach cell `(i, j)`, we must come from:

- Top → (i-1, j)
    
- Left → (i, j-1)
    

If we previously had remainder `r`, then after adding `grid[i][j]`:

`new_r = (r + grid[i][j]) % k`

So:

`dp[i][j][new_r] += dp[i-1][j][r] dp[i][j][new_r] += dp[i][j-1][r]`

This means:

> “Inherit all valid paths from parent cells and update the remainder.”

---

#### 6. Initialization (Starting Point)

At the very first cell (0,0):

`dp[0][0][ grid[0][0] % k ] = 1`

Because there is exactly one way to start: standing there.

---

#### 7. Order of Filling

We fill the table in this order:

- Row by row
    
- Left to right
    

Because each cell depends only on:

- Top cell (already filled)
    
- Left cell (already filled)
    

---

#### 8. Final Answer

The problem asks:

> Number of paths where total sum % k == 0

So the final answer is:

`dp[n-1][m-1][0]`

---

#### ✅ Complete Mental Model (Note-Friendly)

You can write this as your summary:

##### State Definition:

`dp[i][j][r] = number of ways to reach cell (i,j)                such that sum % k = r`

---

##### Transition:

`new_r = (r + grid[i][j]) % k  dp[i][j][new_r] += dp[i-1][j][r] dp[i][j][new_r] += dp[i][j-1][r]`

---

##### Initialization:

`dp[0][0][grid[0][0] % k] = 1`

---

##### Answer:

`dp[n-1][m-1][0]`

---

#### 🔍 Intuition in Simple Words

Each cell acts like a collector of information.  
It says:

> "Through how many ways can I be reached with different remainders?"

Then it passes those ways forward to the next cells.

---

#### 🧩 Real-World Analogy

Imagine money flowing through pipes.  
Each pipe carries different balances (remainders).  
Each cell collects all incoming balances and redistributes them forward.

---

#### 🎯 Why Tabulation Works

- No repeated calculations
    
- No recursion
    
- Each cell knows all valid ways reaching it
    
- Builds solution step-by-step logically
    

---

#### ✅ Time & Space Complexity

`Time:  O(n × m × k) Space: O(n × m × k)`

---

#### ✨ One-line intuition

> Tabulation is just building answers from the start instead of asking recursion to discover them.
## My Approach

- [x] **Works**
#### Memoization

```cpp
class Solution {

public:

    static const int MOD = 1000000007;

  
  

    int yo(vector<vector<int>>& grid,vector<vector<vector<int>>> &dp, int k,int sum,int i,int j){

        int m=grid.size(),n=grid[0].size();

        if(i>=m || j>=n)return 0;

        sum=(sum+grid[i][j])%k;

        if(i==m-1 && j==n-1){

            return sum==0;

        }

        if(dp[i][j][sum]!=-1)return dp[i][j][sum];

        int left=yo(grid,dp,k,sum,i+1,j);

        int right=yo(grid,dp,k,sum,i,j+1);

  

        return dp[i][j][sum]=(left+right)%MOD;

    }

    int numberOfPaths(vector<vector<int>>& grid, int k) {

        int n=grid.size(),m=grid[0].size();

        vector<vector<vector<int>>> dp(

            n, vector<vector<int>>(m, vector<int>(k, -1))

        );

        return yo(grid,dp, k, 0, 0, 0);

    }

};
```


## My Approach 2

- [x] **Works**
#### Tabulation

```cpp
class Solution {

public:

    static const int MOD = 1000000007;

    int numberOfPaths(vector<vector<int>>& grid, int k) {

        int n=grid.size(),m=grid[0].size();

        vector<vector<vector<int>>> dp(

            n, vector<vector<int>>(m, vector<int>(k, 0))

        );

        for(int i=0;i<n;i++){

            for(int j=0;j<m;j++){

                if(i==0 && j==0){dp[i][j][grid[0][0]%k]++;continue;}

                for(int c=0;c<k;c++)

                {

                int a=i-1,b=j;

                if(a>=0 && dp[a][b][c]){

                    dp[i][j][(c + grid[i][j]) % k] =(dp[i][j][(c + grid[i][j]) % k] + dp[a][b][c]) % MOD;

                }

                a++,b--;

                if(b>=0 && dp[a][b][c]){

                    dp[i][j][(c + grid[i][j]) % k] =(dp[i][j][(c + grid[i][j]) % k] + dp[a][b][c]) % MOD;

                }

                }

            }

        }

  

        return dp[n-1][m-1][0];

    }

};
```


## Chat GPT

- [ ] **Works**

```cpp
class Solution {
public:
    static const int MOD = 1000000007;
    vector<vector<vector<int>>> dp;

    int dfs(vector<vector<int>>& grid, int i, int j, int rem, int k) {
        int n = grid.size(), m = grid[0].size();

        if(i >= n || j >= m) return 0;

        rem = (rem + grid[i][j]) % k;

        if(i == n-1 && j == m-1)
            return rem == 0;

        if(dp[i][j][rem] != -1)
            return dp[i][j][rem];

        long long ways = 0;
        ways += dfs(grid, i+1, j, rem, k);
        ways += dfs(grid, i, j+1, rem, k);

        return dp[i][j][rem] = ways % MOD;
    }

    int numberOfPaths(vector<vector<int>>& grid, int k) {
        int n = grid.size(), m = grid[0].size();
        dp.assign(n, vector<vector<int>>(m, vector<int>(k, -1)));
        return dfs(grid, 0, 0, 0, k);
    }
};

```



```cpp
class Solution {
public:
    static const int MOD = 1000000007;

    int numberOfPaths(vector<vector<int>>& grid, int k) {
        int n = grid.size(), m = grid[0].size();

        vector<vector<vector<int>>> dp(
            n, vector<vector<int>>(m, vector<int>(k, 0))
        );

        dp[0][0][grid[0][0] % k] = 1;

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(i == 0 && j == 0) continue;

                for(int r = 0; r < k; r++){
                    int val = grid[i][j];

                    if(i > 0){
                        dp[i][j][(r + val) % k] =
                        (dp[i][j][(r + val) % k] + dp[i-1][j][r]) % MOD;
                    }

                    if(j > 0){
                        dp[i][j][(r + val) % k] =
                        (dp[i][j][(r + val) % k] + dp[i][j-1][r]) % MOD;
                    }
                }
            }
        }

        return dp[n-1][m-1][0];
    }
};

```

#### Some space optimised DP it seems
```cpp
class Solution {
public:
    static const int MOD = 1000000007;

    int numberOfPaths(vector<vector<int>>& grid, int k) {
        int n = grid.size(), m = grid[0].size();

        vector<vector<int>> prev(m, vector<int>(k, 0)), curr(m, vector<int>(k, 0));
        prev[0][grid[0][0] % k] = 1;

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(i==0 && j==0) continue;

                fill(curr[j].begin(), curr[j].end(), 0);

                for(int r = 0; r < k; r++){
                    if(i > 0)
                        curr[j][(r + grid[i][j]) % k] =
                        (curr[j][(r + grid[i][j]) % k] + prev[j][r]) % MOD;

                    if(j > 0)
                        curr[j][(r + grid[i][j]) % k] =
                        (curr[j][(r + grid[i][j]) % k] + curr[j-1][r]) % MOD;
                }
            }
            prev = curr;
        }

        return prev[m-1][0];
    }
};

```