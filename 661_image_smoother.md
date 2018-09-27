## 思路
直觉
```c++
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& M) 
    {
        int row = M.size(), col = M[0].size();
        vector<vector<int>> dirs = {{0,1}, {0,-1}, {1,0}, {-1,0}, {-1,-1}, {-1,1}, {1,-1}, {1,1}};
        //vector<vector<int>> res(M); // 正确
        //vector<vector<int>> res[row][col]; //错误
        vector<vector<int>> res(row, vector<int>(col, 0)); //正确，初始化为0
        for(int i=0; i<row; ++i)
            for(int j=0; j<col; ++j)
            {
                int count = 1;
                int sum = M[i][j];
                for(int n=0; n<8; ++n)
                {
                    int x = i+dirs[n][0];
                    int y = j+dirs[n][1];
                    if(x>=0 && x<row && y>=0 && y<col)
                    {
                        sum += M[x][y];
                        ++count;
                    }
                }
                res[i][j] = sum/count;
            
            }
        return res;
    }
};
```
**关于二维向量初始化的问题：**

比如要初始化一个row*col的二维向量，让其所有值为0.

方法一：直接初始化
```c++
vector<vector<int>> res(row, vector<int>(col, 0));
```

方法二：resize()控制大小
```c++
vector<vector<int>> res;
res.resize(row);//row行
for (int i = 0; i < row; ++i)
    res[k].resize(c);//col列
```
