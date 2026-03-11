## Problem Link [Here]([662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/))
## Tags #Medium 
## Related Problems

## Topics [[Trees]]

## Solutions


## Striver Approach

- [ ] **Works**

```cpp
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if(!root) return 0;

        long long ans = 0;
        queue<pair<TreeNode*, long long>> q;
        q.push({root, 0});

        while(!q.empty()) {
            int size = q.size();
            long long minIndex = q.front().second;
            long long first, last;

            for(int i = 0; i < size; i++) {
                auto [node, idx] = q.front();
                q.pop();

                idx -= minIndex;   // normalize index

                if(i == 0) first = idx;
                if(i == size - 1) last = idx;

                if(node->left)
                    q.push({node->left, idx * 2 + 1});

                if(node->right)
                    q.push({node->right, idx * 2 + 2});
            }

            ans = max(ans, last - first + 1);
        }

        return ans;
    }
};
```


## Claude

- [ ] **Works**

```cpp
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if (!root) return 0;
        
        int maxWidth = 0;
        // Store {node, index_at_this_level}
        queue<pair<TreeNode*, long long>> q;
        q.push({root, 0});
        
        while (!q.empty()) {
            int size = q.size();
            long long levelStart = q.front().second; // normalize to prevent overflow
            long long first = 0, last = 0;
            
            for (int i = 0; i < size; i++) {
                auto [node, idx] = q.front();
                q.pop();
                
                // Normalize index relative to level start
                long long normalizedIdx = idx - levelStart;
                
                if (i == 0) first = normalizedIdx;
                if (i == size - 1) last = normalizedIdx;
                
                if (node->left)
                    q.push({node->left, 2 * normalizedIdx});
                if (node->right)
                    q.push({node->right, 2 * normalizedIdx + 1});
            }
            
            maxWidth = max(maxWidth, (int)(last - first + 1));
        }
        
        return maxWidth;
    }
};
```


## Approach 2

- [ ] **Works**

```cpp

```