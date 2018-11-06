## 思路
数组中总的元素的和`sum`是一定的，可以从左往右移动索引，判断索引左侧元素的和`sumLeft`是否等于索引右侧元素的和`sum-sumLetf-nums[index]`。
或`2*sumLetf`是否等于`sum-nums[index]`。

#### Java
```java
class Solution {
    public int pivotIndex(int[] nums) 
    {
        int sum = 0;
        int leftSum = 0;
        for(int x:nums)
            sum +=x;
        
        for(int i=0; i<nums.length; i++)
        {
            if(leftSum == sum - leftSum - nums[i])
                return i;
            leftSum +=nums[i];
        }
        return -1;
    }
}
```
