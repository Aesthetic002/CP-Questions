## Problem Link [Here](https://leetcode.com/submissions/detail/1830306189/)

### Related Problems

### Topics


## My Approach

```cpp

class Solution {
public:
    bool dfs(vector<vector<char>>& board, vector<vector<int>>&vis,string &word,int i,int j,int index){
        int n=board.size(),m=board[0].size();
        
        if(board[i][j]!=word[index]){
            return false;
        }
        if(index>=word.size()-1)return true;
        vis[i][j]=1;
        int hor[]={0,1,0,-1};
        int ver[]={-1,0,1,0};

        for(int k=0;k<4;k++){
            int a=ver[k] + i;
            int b= hor[k] + j;
            
            if(a<n && a>=0 && b<m && b>=0 && !vis[a][b])
            {
                if(dfs(board,vis,word,a,b,index+1))
                    return true;

                vis[a][b]=0;
            }
        }
        return false;
    }

    bool exist(vector<vector<char>>& board, string word) {
        int n=board.size(),m=board[0].size();
        vector<vector<int>>vis(n,vector<int>(m,0));
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(!vis[i][j]){
                    int index=0;
                    if(dfs(board,vis,word,i,j,index))
                        return true;
                    vis[i][j]=0;
                }
            }
        }

        return false;
    }
};
```


## Approach 1

```cpp

```


## Approach 2

```cpp

```