## Java
```java
class Solution {
    public int findLengthOfLCIS(int[] nums) 
    {
        if(nums.length == 0)
            return 0;
        
        int res = 1;
        int tmp = 1;
        for(int i=0; i<nums.length-1; i++)
        {
            if(nums[i] < nums[i+1])
            {
                tmp++;
                res = Math.max(tmp, res);
            }
            else
                tmp = 1;
        }
        
        return res;
    }
}

```
注意判断当数组长度为0时的情况。

