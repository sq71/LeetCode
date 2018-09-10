```
class Solution {
public:
    vector<vector<int>> flipAndInvertImage(vector<vector<int>>& A) 
    {
        int size;
        int sum;
        size = A.size();
        for(int i=0; i<size; ++i)
        {
            for(int j=0; j<size/2; ++j)
            {
                sum = A[i][j] + A[i][size-1-j];
                A[i][j] = sum - A[i][j];
                A[i][size-1-j] = sum - A[i][j];
            }
 
        }
        for(int i =0; i<size; ++i)
        {
            for(int j=0; j<size; j++)
            {
                    A[i][j] ^= 1;    
            }
        }
 
    return A;    
    }
};
```
