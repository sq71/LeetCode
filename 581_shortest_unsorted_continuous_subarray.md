## 思路
#### 方法1： Brute Force [Time Limit Exceeded]
虽然没ac但是也有值得思考和借鉴的地方。

要判断一个区间[i, j)是否满足题意，需要满足以下条件：

1) 对于[i, j)内的最大值、最小值`max`、`min`，`nums[i-1]`小于`min`，并且`nums[j]`大于`max`;

2) [0, i)内元素递增;

3) [j, n)内元素递增.

```java
// java
class Solution {
    public int findUnsortedSubarray(int[] nums) 
    {
        int n = nums.length;
        int res = n;
        for(int i=0; i<n; i++)
        {
            for(int j=i; j<=n; j++)
            {
                int min=Integer.MAX_VALUE, max = Integer.MIN_VALUE, prev=Integer.MIN_VALUE;
                for(int k=i; k<j; k++)
                {
                    min = Math.min(min, nums[k]);
                    max = Math.max(max, nums[k]);
                }
                
                // nums[i-1]小于min，并且nums[j]大于max (否则继续循环)
                if((i>0 && nums[i-1]>min) || (j<n && nums[j]<max))
                    continue;
                
                // 判断 [0, i)是否递增 (否则继续循环)
                int k=0;
                while(k<i && prev<=nums[k]) 
                {
                    prev = nums[k];
                    k++;
                }
                if(k != i)
                    continue;
                // 判断[j, n)是否递增
                k = j;
                while(k<n && prev<=nums[k])
                {
                    prev = nums[k];
                    k++;
                }
                if(k == nums.length)
                {
                    res = Math.min(res, j-i);
                }
            }
        }
        
        return res;
    }
}
```

#### 改进1：Better Brute Force [Accepted]
基于选择排序的思路。遍历数组元素nums[i]，比较其后的每一个元素nums[j]，即满足i<j<n。

如果nums[j]<nums[i],说明区间[i,j]中的元素需要重排，
需要找到所有这种区间中，最左边边界i_min和最右边边界j_max,
区间[i_min, j_max]即为真正需要重排的区间。
```java
//java
class Solution {
    public int findUnsortedSubarray(int[] nums) 
    {
        int n=nums.length;
        int left = n, right = 0;
        for(int i=0; i<n-1; i++)
        {
            for(int j=i+1; j<n; j++)
            {
                if(nums[j] < nums[i])
                {
                    right = Math.max(right, j);
                    left = Math.min(left, i);
                }
            }
        }
        //return right-left == -n ? 0 : right-left+1;
        return right-left < 0 ? 0 : right-left+1;
    }
}
```


