## 思路
遍历一遍数组，找到最大和第二大的元素。

#### Java
```java
class Solution {
    public int dominantIndex(int[] nums) 
    {
        
        int n = nums.length;
        int maxMax = nums[0];
        int max = -1;
        int index = 0;
        
        if(n == 1)
            return 0;
        
        for(int i=1; i<n; i++)
        {
            if(nums[i] > maxMax)
            {
                max = maxMax;
                maxMax = nums[i];
                index = i;
            }
            else if(nums[i] > max)
            {
                max = nums[i];
            }
        }
        
        return maxMax >= 2*max ?  index : -1;
        
        
    }
}
```

