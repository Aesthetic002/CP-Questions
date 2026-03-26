## Problem Link [Here](https://leetcode.com/problems/equal-sum-grid-partition-ii/description/?envType=daily-question&envId=2026-03-26)
## Tags #Hard 
## Related Problems

## Topics [[Prefix Sum]] [[Maps]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    bool canPartitionGrid(vector<vector<int>>& grid) {
        long long n = grid.size(), m = grid[0].size();
        vector<long long> yo1, yo2;
        unordered_map<long long, long long> baap;

        // Building yo1
        for (long long i = 0; i < n; i++) {
            long long pd = 0;
            for (long long j = 0; j < m; j++) {
                pd = pd + grid[i][j];
                baap[grid[i][j]]++;
            }
            yo1.push_back(pd);
        }
        // Building yo2
        for (long long j = 0; j < m; j++) {
            long long pd = 0;
            for (long long i = 0; i < n; i++) {
                pd = pd + grid[i][j];
            }
            yo2.push_back(pd);
        }

        // Horizontal Cuts

        // Building pref1 and suf1
        vector<long long> pref1(n), suf1(n);
        unordered_map<long long, long long> mp1, mp2;
        mp2 = baap;
        pref1[0] = yo1[0];
        suf1[n - 1] = 0;

        for (long long i = 1; i < n - 1; i++) {
            pref1[i] = pref1[i - 1] + yo1[i];
        }
        for (long long i = n - 1; i > 0; i--) {
            suf1[i - 1] = suf1[i] + yo1[i];
        }

        if (n == 2 && m > 1) {
            mp1[grid[0][0]]++;
            mp1[grid[0][m - 1]]++;
            for (long long j = 0; j < m; j++) {
                mp2[grid[0][j]]--;
                if (!mp2[grid[0][j]])
                    mp2.erase(grid[0][j]);
            }
            for (long long j = 1; j < m - 1; j++) {
                mp2[grid[n - 1][j]]--;
                if (!mp2[grid[n - 1][j]])
                    mp2.erase(grid[n - 1][j]);
            }
            if (suf1[0] && pref1[0] &&
                ((pref1[0] == suf1[0]) ||
                 (mp1.find(pref1[0] - suf1[0]) != mp1.end()) ||
                 (mp2.find(suf1[0] - pref1[0]) != mp2.end())))
                return true;
        }

        else if (n > 2 && m > 1) { // Test for i=0
            mp1[grid[0][0]]++;
            mp1[grid[0][m - 1]]++;
            for (long long j = 0; j < m; j++) {
                mp2[grid[0][j]]--;
                if (!mp2[grid[0][j]])
                    mp2.erase(grid[0][j]);
            }

            if (suf1[0] && pref1[0] &&
                ((pref1[0] == suf1[0]) ||
                 (mp1.find(pref1[0] - suf1[0]) != mp1.end()) ||
                 (mp2.find(suf1[0] - pref1[0]) != mp2.end())))
                return true;
            for (long long j = 1; j < m - 1; j++)
                mp1[grid[0][j]]++;

            for (long long i = 1; i < n - 1; i++) {
                // Fill mp1 and erase mp2 from j->0 to j->m-1
                for (long long j = 0; j < m; j++) {
                    mp1[grid[i][j]]++;
                    mp2[grid[i][j]]--;
                    if (!mp2[grid[i][j]])
                        mp2.erase(grid[i][j]);
                }
                if (i == n - 2) {
                    for (long long j = 1; j < m - 1; j++) {
                        mp2[grid[n - 1][j]]--;
                        if (!mp2[grid[n - 1][j]])
                            mp2.erase(grid[n - 1][j]);
                    }
                }
                if (suf1[i] && pref1[i] &&
                    ((pref1[i] == suf1[i]) ||
                     (mp1.find(pref1[i] - suf1[i]) != mp1.end()) ||
                     (mp2.find(suf1[i] - pref1[i]) != mp2.end())))
                    return true;
            }
        }
        // Vertical Cuts

        // Building pref2 and suf2
        vector<long long> pref2(m), suf2(m);
        unordered_map<long long, long long> mp3, mp4;
        mp4 = baap;
        pref2[0] = yo2[0];
        suf2[m - 1] = 0;

        for (long long i = 1; i < m - 1; i++) {
            pref2[i] = pref2[i - 1] + yo2[i];
        }
        for (long long i = m - 1; i > 0; i--) {
            suf2[i - 1] = suf2[i] + yo2[i];
        }

        if (m == 2 && n > 1) {
            mp3[grid[0][0]]++;
            mp3[grid[n - 1][0]]++;
            for (long long i = 0; i < n; i++) {
                mp4[grid[i][0]]--;
                if (!mp4[grid[i][0]])
                    mp4.erase(grid[i][0]);
            }
            for (long long i = 1; i < n - 1; i++) {
                mp4[grid[i][m - 1]]--;
                if (!mp4[grid[i][m - 1]])
                    mp4.erase(grid[i][m - 1]);
            }
            if (suf2[0] && pref2[0] &&
                ((pref2[0] == suf2[0]) ||
                 (mp3.find(pref2[0] - suf2[0]) != mp3.end()) ||
                 (mp4.find(suf2[0] - pref2[0]) != mp4.end())))
                return true;
        } else if (m > 2 && n > 1) {
            // Test for j=0
            mp3[grid[0][0]]++;
            mp3[grid[n - 1][0]]++;
            for (long long i = 0; i < n; i++) {
                mp4[grid[i][0]]--;
                if (!mp4[grid[i][0]])
                    mp4.erase(grid[i][0]);
            }

            if (suf2[0] && pref2[0] &&
                ((pref2[0] == suf2[0]) ||
                 (mp3.find(pref2[0] - suf2[0]) != mp3.end()) ||
                 (mp4.find(suf2[0] - pref2[0]) != mp4.end())))
                return true;
            for (long long i = 1; i < n - 1; i++)
                mp3[grid[i][0]]++;

            for (long long j = 1; j < m - 1; j++) {
                // Fill mp1 and erase mp2 from j->0 to j->m-1
                for (long long i = 0; i < n; i++) {
                    mp3[grid[i][j]]++;
                    mp4[grid[i][j]]--;
                    if (!mp4[grid[i][j]])
                        mp4.erase(grid[i][j]);
                }
                if (j == m - 2) {
                    for (long long i = 1; i < n - 1; i++) {
                        mp4[grid[i][m - 1]]--;
                        if (!mp4[grid[i][m - 1]])
                            mp4.erase(grid[i][m - 1]);
                    }
                }
                if (suf2[j] && pref2[j] &&
                    ((pref2[j] == suf2[j]) ||
                     (mp3.find(pref2[j] - suf2[j]) != mp3.end()) ||
                     (mp4.find(suf2[j] - pref2[j]) != mp4.end())))
                    return true;
            }
        }
        if (n == 1) {
            // evaluate yo2
            // i==0
            if (suf2[0] && pref2[0] && pref2[0] == suf2[0])
                return true;
            for (long long i = 1; i < m - 2; i++) {
                if (suf2[i] && pref2[i] &&
                    ((pref2[i] == suf2[i]) || (pref2[i] - suf2[i] == yo2[0]) ||
                     (pref2[i] - suf2[i] == yo2[i]) ||
                     (suf2[i] - pref2[i] == yo2[m - 1]) ||
                     (suf2[i] - pref2[i] == yo2[i + 1])))
                    return true;
            }
            // i==m-1
            if (suf2[m - 2] && pref2[m - 2] &&
                ((pref2[m - 2] == suf2[m - 2]) ||
                 (pref2[m - 2] - suf2[m - 2] == yo2[0]) ||
                 (pref2[m - 2] - suf2[m - 2] == yo2[m - 2])))
                return true;
        }
        if (m == 1) {
            // evaluate yo1
            // i==0
            if (suf1[0] && pref1[0] && pref1[0] == suf1[0])
                return true;
            for (long long i = 1; i < n - 2; i++) {
                if (suf1[i] && pref1[i] &&
                    ((pref1[i] == suf1[i]) || (pref1[i] - suf1[i] == yo1[0]) ||
                     (pref1[i] - suf1[i] == yo1[i]) ||
                     (suf1[i] - pref1[i] == yo1[n - 1]) ||
                     (suf1[i] - pref1[i] == yo1[i + 1])))
                    return true;
            }
            // i==n-1
            if (suf1[n - 2] && pref1[n - 2] &&
                ((pref1[n - 2] == suf1[n - 2]) ||
                 (pref1[n - 2] - suf1[n - 2] == yo1[n - 2]) ||
                 (pref1[n - 2] - suf1[n - 2] == yo1[0])))
                return true;
        }
        return false;
    }
};
```


## Chat GPT Approach

- [x] **Works**

```cpp
class Solution {
public:
    bool canPartitionGrid(vector<vector<int>>& grid) {
        long long m = grid.size(), n = grid[0].size();
        
        long long total = 0;
        for (auto &row : grid)
            for (long long x : row)
                total += x;

        // ---------- HORIZONTAL ----------
        unordered_map<long long,long long> bottom;
        for (auto &row : grid)
            for (long long x : row)
                bottom[x]++;

        unordered_map<long long,long long> top;

        long long topSum = 0;

        for (long long i = 0; i < m - 1; i++) {
            for (long long j = 0; j < n; j++) {
                long long val = grid[i][j];
                top[val]++;
                bottom[val]--;
                if (bottom[val] == 0) bottom.erase(val);
                topSum += val;
            }

            long long bottomSum = total - topSum;

            if (topSum == bottomSum) return true;

            long long diff = abs(topSum - bottomSum);

            if (topSum > bottomSum) {
                if (valid(top, grid, 0, i, 0, n-1, diff))
                    return true;
            } else {
                if (valid(bottom, grid, i+1, m-1, 0, n-1, diff))
                    return true;
            }
        }

        // ---------- VERTICAL ----------
        unordered_map<long long,long long> right;
        for (auto &row : grid)
            for (long long x : row)
                right[x]++;

        unordered_map<long long,long long> left;

        long long leftSum = 0;

        for (long long j = 0; j < n - 1; j++) {
            for (long long i = 0; i < m; i++) {
                long long val = grid[i][j];
                left[val]++;
                right[val]--;
                if (right[val] == 0) right.erase(val);
                leftSum += val;
            }

            long long rightSum = total - leftSum;

            if (leftSum == rightSum) return true;

            long long diff = abs(leftSum - rightSum);

            if (leftSum > rightSum) {
                if (valid(left, grid, 0, m-1, 0, j, diff))
                    return true;
            } else {
                if (valid(right, grid, 0, m-1, j+1, n-1, diff))
                    return true;
            }
        }

        return false;
    }

    bool valid(unordered_map<long long,long long>& freq,
               vector<vector<int>>& grid,
               long long r1, long long r2, long long c1, long long c2,
               long long diff) {

        if (freq.find(diff) == freq.end()) return false;

        long long rows = r2 - r1 + 1;
        long long cols = c2 - c1 + 1;

        // 2D block → safe
        if (rows > 1 && cols > 1) return true;

        // 1D strip → check edges only
        if (rows == 1) {
            return grid[r1][c1] == diff || grid[r1][c2] == diff;
        } else {
            return grid[r1][c1] == diff || grid[r2][c1] == diff;
        }
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```