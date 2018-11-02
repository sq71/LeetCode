## 动态规划

令sum[i]是从i开始到数组末端的子串的和。则递推公式为：`sum[i] = max(nums[i], nums[i]+sum[i+1])`。

递推公式只用到后一项，所以可以状态压缩，用一个变量即可。

#### java

```java
class Solution {
    public int maxSubArray(int[] nums) 
    {
        int n = nums.length;
        int sum = nums[n-1];
        int maxSum = nums[n-1];
        for(int i=n-2; i>=0; i--)
        {
            sum = Math.max(nums[i], nums[i]+sum);
            maxSum = Math.max(sum, maxSum);
        }
        
        return maxSum;
    }
}
```
