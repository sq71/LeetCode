## 方法一
分三个部分计算：
1. 计算数组首部连续零的数量，`res = max(res, zeros)`
2. 计算数组中间连续零的数量， `res = max(res, (zeros+1)/2)`
3. 计算数组尾部连续零的数量， `res = max(res, zeros)`

#### Java
```java
class Solution {
    public int maxDistToClosest(int[] seats) 
    {
        int n=seats.length;
        int res = 0;
        int i, j;
        
        for(i=0, j=0; j<n; j++)
        {
            if(seats[j] == 1)
            {
                if(i == 0)
                    res = Math.max(j-i, res);
                else
                    res = Math.max((j-i+1)/2, res);
                 
                i = j+1;
            }
        }
        
        res = Math.max(j-i, res);
        return res;
    }
}
```
注意思考为什么j-i为两个索引间0的数量。

## 方法二
类似方法一，另一种索引移动方式。
#### Java
```java
class Solution {
    public int maxDistToClosest(int[] nums) 
    {
        int n = nums.length;
        int max = 0;
        int i = 0;
        while(i < n)
        {
            while(i < n && nums[i] == 1) //找到从左往右第一个为0的位置
            {
                i++;
            }
            int j = i;//start  //j定位在0上
            while(i < n && nums[i] == 0) //再找到从左往右下一个为1的位置
            {
                i++;
            }
            if(j == 0 || i == n) //如果此段0串在数组首端或者尾端
            {
                max = Math.max(max, i - j);
            }
            else //在数组中间的0串
            {
                max = Math.max(max, (i - j + 1) / 2) ;
            }
        }
        return max;
    }
}
```
