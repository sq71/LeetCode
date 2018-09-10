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
```
