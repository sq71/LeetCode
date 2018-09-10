两层循环。
```
class Solution {
public:
    vector<vector<int>> transpose(vector<vector<int>>& A) 
    {
        vector<vector<int> > res;  
        int row, col;
        row = A.size();
        col = A[0].size();
        for(int i = 0; i < col; ++i)
        {
            vector<int> temp;
            for(int j=0; j< row; ++j)
                temp.push_back(A[j][i]);
            res.push_back(temp);
        }
        return res;
    }
};
```
