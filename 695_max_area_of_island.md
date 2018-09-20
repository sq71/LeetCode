## 思路
#### 方法1：
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
结果会超时! 因为数组越界。

下面部分如果加上if语句，Runtime: 36 ms -> 16 ms

应该是输入矩阵比较稀疏，0比较多，每次0的时候都要有一次函数调用，调用的时候代价比直接判断一次多费很多时钟周期。
```
for(int i=0; i<grid.size(); ++i)
    for(int j=0; j<grid[0].size(); j++)
    {
        if(grid[i][j] == 1)
        {
            max = dfs(grid, i, j)
            if(max > res)
                res = max;
        }
        
    }
```

#### 方法2:
bfs
```
class Solution {
public:    
    int bfs(vector<vector<int> >& grid, int i, int j)
    {
        int max=0;
        queue<pair<int, int>> myq;
        myq.push({i, j});
        
        while(!myq.empty())
        {
            int a = myq.front().first;
            int b = myq.front().second;
            myq.pop();

            if(a>=0 && a<grid.size() && b>=0 && b<grid[0].size() && grid[a][b]==1)
            {
                max++;                
                grid[a][b] = 0;                
                myq.push({a-1,b});
                myq.push({a+1,b});
                myq.push({a,b-1});
                myq.push({a,b+1});

            }
        }
        
        return max;
    }    

    int maxAreaOfIsland(vector<vector<int>>& grid) 
    {
        int res = 0;
        int max;
        
        for(int i=0; i<grid.size(); ++i)
            for(int j=0; j<grid[0].size(); ++j)
            {
                if (grid[i][j] == 1)
                {
                    max = bfs(grid, i, j);
                    res = res>max ? res : max;
                }
            }
        return res;
    }
    
};
```
