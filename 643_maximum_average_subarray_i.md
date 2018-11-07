## 方法1： 使用滑动窗口（Sliding Window）
#### 初始代码 [Time Limit Exceeded]
```java
// java
class Solution {
    public double findMaxAverage(int[] nums, int k) 
    {
        double res = -Double.MAX_VALUE; //Double.MAX_VALUE表示Double里的最大值，
                                        //Double.MIN_VALUE表示Double里正数里的最小值。
        int n = nums.length;        
        for(int i=0; i<n-k+1; ++i)
        {
            double sum = 0.0;
            for(int j=0; j<k; ++j)
                sum += nums[i+j];
            
            res = Math.max(res, sum/k);
        }   
        return res;
    }
}
```
超出时限的原因应该是使用了两层for循环，当k值比较大时，耗时严重。
#### 修改代码 [Accepted]
```java
//java
class Solution {
    public double findMaxAverage(int[] nums, int k) 
    {
        int n = nums.length;
        double sum = 0;
        for(int i=0; i<k; ++i)
            sum += nums[i];
        
        double res = sum;
        for(int i=k; i<nums.length; ++i)
        {
            sum += nums[i]-nums[i-k];
            res = Math.max(res, sum);
        }
        
        return res/k;
    }
}
```
时间复杂度：*O(n)*

空间复杂度：*O(1)*

## 方法2：累积总和（Cumulative Sum）
创建一个新数组sum[n],sum[i]表示前i项的总和,则以i结尾的K项之和为`res=sum[i]-sum[i-k]`。

代码：[Accepted]
```java
// java
class Solution {
    public double findMaxAverage(int[] nums, int k) 
    {
        int n = nums.length;
        int[] sum = new int[n];
        
        sum[0] = nums[0];
        for(int i=1; i<n; i++)
            sum[i] = sum[i-1]+nums[i];
        
        double res = sum[k-1];

        for(int i=k; i<n; ++i)
            res = Math.max(res, sum[i]-sum[i-k]);
        
        return res / k;
    }
}
```

