## Problem Link [Here](https://leetcode.com/problems/combination-sum-ii/)

### Related Problems

### Topics


## My Approach

```cpp

```


## Approach 1

```cpp
class Solution {
public:
    vector<vector<int>> ans;

    void yo(vector<int>& c, int target, vector<int>& temp, int index) {

        // If target becomes zero, we found a combination.
        if (target == 0) {
            ans.push_back(temp);
            return;
        }

        // Loop through all candidates starting from current index
        for (int i = index; i < c.size(); i++) {

            // ❌ Skip duplicates at the same recursion level
            if (i > index && c[i] == c[i - 1]) 
                continue;

            // No need to continue if number is bigger than target
            if (c[i] > target) 
                break;

            // ✔️ Choose this number
            temp.push_back(c[i]);

            // Go deeper, but i+1 because each number can be used once
            yo(c, target - c[i], temp, i + 1);

            // ✔️ Undo the choice (backtrack)
            temp.pop_back();
        }
    }

    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());  // sorting helps skip duplicates
        vector<int> temp;
        yo(candidates, target, temp, 0);
        return ans;
    }
};

```


## Approach 2

```cpp

```