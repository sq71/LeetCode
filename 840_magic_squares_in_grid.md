## 思路
满足题意的九宫格：
中间格子是5；所有格子包含1~9九个数字；第1、3行，1、3列，两条斜对角线之和都为15.

#### Java
```java
class Solution {
    public int numMagicSquaresInside(int[][] grid) 
    {
        int row = grid.length;
        int col = grid[0].length;
        int res = 0;

        for(int i=0; i<row-2; i++)
            for(int j=0; j<col-2; j++)
            {
                if(Judge(grid, i, j) == true)
                    res++;
            }
        
        return res;
    }
    
     boolean Judge(int[][] grid, int row, int col)
        {
            if(grid[row+1][col+1] != 5)
                return false;
            
            int[] tmp = new int[16];
            for(int i=row; i<row+3; i++)
                for(int j=col; j<col+3; j++)
                    tmp[grid[i][j]] = 1;
            for(int i=1; i<10; i++)
                if(tmp[i] == 0)
                    return false;
            
            if(grid[row][col]+grid[row+1][col+1]+grid[row+2][col+2] != 15) return false;
            if(grid[row][col+2]+grid[row+1][col+1]+grid[row+2][col] != 15) return false;
            if(grid[row][col]+grid[row][col+1]+grid[row][col+2] != 15) return false;
            if(grid[row+2][col]+grid[row+2][col+1]+grid[row+2][col+2] != 15) return false;
            if(grid[row][col]+grid[row][col+1]+grid[row][col+2] != 15) return false;
            if(grid[row][col+2]+grid[row+1][col+2]+grid[row+2][col+2] != 15) return false;
            
            return true;
        }
}
```
