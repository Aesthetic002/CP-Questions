## Problem Link [Here](https://leetcode.com/problems/leaf-similar-trees/description/?envType=problem-list-v2&envId=binary-tree)
## Tags #Easy 
## Related Problems

## Topics [[Trees]]

## Solutions


## My Approach

- [x] **Works**

```cpp
class Solution {
public:
    void preorder(TreeNode* root,vector<int>&a1){
        if(!root)return;
        if(!root->left && !root->right)a1.push_back(root->val);
        preorder(root->left,a1);
        preorder(root->right,a1);
    }
    bool leafSimilar(TreeNode* root1, TreeNode* root2) {
        vector<int>a1,a2;
        preorder(root1,a1);
        preorder(root2,a2);

        return a1==a2;
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