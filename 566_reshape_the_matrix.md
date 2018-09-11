## 思路
原：
```
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) 
    {
        int n = nums.size();
        int m = nums[0].size();
        if(n*m != r*c)
            return nums;
        
        vector<int> temp1;
        for(int i=0; i<n; i++)
            for(int j=0; j<m; j++)
                temp1.push_back(nums[i][j]);

        vector<vector<int>> res;
        for(int i=0; i<r; i++)
        {
            vector<int> temp2;        
            
            for(int j=0; j<c; j++)
                temp2.push_back(temp1[c*i+j]);
            
            res.push_back(temp2);
        }
                
        return res;
    }
};
// Runtime: 40 ms	
```

改进：
```
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) 
    {
        int m = nums.size(); 
        int n = nums[0].size();
        if(m * n != r * c) 
            return nums;
        vector<vector<int>> res(r, vector<int>(c)); //声明一个r行c列的vector
        int row = 0, col = 0;
        for(int i = 0; i < r; ++i)
            for(int j = 0; j < c; ++j)
            {
                /* or   //Runtime:40 ms
                res[i][j] = nums[row][col++];
                if(col == n) 
                {
                    col = 0;
                    row++;  
                }
                */
                res[i][j] = nums[(i*c+j) / n][(i*c+j) % n];  //Runtime: 24 ms
            }
        return res;
    }
};
```
