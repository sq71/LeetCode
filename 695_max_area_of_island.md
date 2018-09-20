## 思路
dfs

```
class Solution {
public:
    
    int dfs(vector<vector<int> >& grid, int i, int j)
    {
        if(i>=0 && i<grid.size() && j>=0 && j<grid[0].size() && grid[i][j] == 1)
        {
            grid[i][j] = 0;
            return 1 + dfs(grid, i-1, j) + dfs(grid, i+1, j) + dfs(grid, i, j-1) + dfs(grid, i, j+1);
        }
        return 0;
    }    
    
    
    
    int maxAreaOfIsland(vector<vector<int>>& grid) 
    {
        int res = 0;
        int max = 0;
        for(int i=0; i<grid.size(); ++i)
            for(int j=0; j<grid[0].size(); j++)
            {
                max = dfs(grid, i, j);
                if(max > res)
                    res = max;
            }
        return res;
    }
    
};
```
注意：如果if(i>=0 && i<grid.size() && j>=0 && j<grid[0].size() && grid[i][j] == 1)写成
if(grid[i][j] == 1 && i>=0 && i<grid.size() && j>=0 && j<grid[0].size())
结果会超时。

（可能是grid[i][j] == 1访问速度慢？why?）
