## Problem Link [Here](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/)

### Related Problems

### Topics


## My Approach


Passed LeetCode Hard

```cpp
class Solution {

public:

    map<int,vector<TreeNode*>>mp;

    map<TreeNode*,int>cmp;

    int left=0,right=0;

    void yo(int height,int width,TreeNode* root){

        if(!root)return;

        mp[width].push_back(root);

        cmp[root]=height;

        left=min(left,width);

        right=max(right,width);

  

        yo(height+1,width-1,root->left);

        yo(height+1,width+1,root->right);

  

    }

    vector<vector<int>> verticalTraversal(TreeNode* root) {

        yo(0,0,root);

        vector<vector<int>>ans;

  

        for(int i=left;i<=right;i++){

            //mp[i]---->arr

            for(int j=0;j<mp[i].size()-1;j++){

                for(int k=0;k<mp[i].size()-1-j;k++){

                    if(cmp[(mp[i][k])]>cmp[(mp[i][k+1])]){

                        swap(mp[i][k],mp[i][k+1]);

                    }

                    else if(cmp[(mp[i][k])]==cmp[(mp[i][k+1])]){

                        if((mp[i][k])->val > (mp[i][k+1])->val ){

                            swap(mp[i][k],mp[i][k+1]);

                        }

                    }

                }

            }

  
  

            vector<int>hehe;

            for(auto z:mp[i]){

                hehe.push_back(z->val);

            }

            ans.push_back(hehe);

        }

  

// for (auto it = cmp.begin(); it != cmp.end(); ++it) {

//     cout << it->first << " : " << it->second << "\n";

// }

  

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