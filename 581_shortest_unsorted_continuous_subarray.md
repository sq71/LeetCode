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

#### 方法1改进1：Better Brute Force [Accepted]
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

#### 方法2：使用排序的方法 [Accepted]
复制一个数组snums[]并对其排序，比较snums[]与nums[]，设两数组最左端开始与最右端开始不同的元素分别是a,b。则[a, b]
即为需要重排的数组。
```java
//java
class Solution {
    public int findUnsortedSubarray(int[] nums)
    {
        int n = nums.length;
        int[] snums = nums.clone();
        Arrays.sort(snums);
        int a=n, b=0;
        for(int i=0; i<n; i++)
        {
            if(nums[i] != snums[i])
            {
                a = Math.min(i, a);
                b = Math.max(i, b);
            }

        }
        return a>b ? 0 : b-a+1;
    }
}
```
#### 方法3：使用栈[Accepted]
这种方法也是基于选择排序，需要确定未排序的子数组中最小和最大元素的正确位置，以确定所求的未排序子数组的边界。

使用栈来实现算法。从前往后遍历nums数组，对于升序排列的元素，不断地将元素的索推入栈内；一旦遇到比堆栈顶部的元素小的元素nums[j]，说明nums[j]不在它的正确位置。

为了确定其正确位置，不断地从栈顶弹出元素，直到栈顶元素对应索引小于j。设此时栈顶索引为k，停止弹出。现在NUMS[j]找到了它的正确位置，它需要处在索引为K+ 1的位置。

遍历整个数组时遵循相同的过程，并确定最小此类k的值。kmin标志着未排序子阵列的左边界。

类似地，为了找到未排序子数组的右边界，向后遍历numsnums数组，找到kmax。

```java
//java
class Solution {
    public int findUnsortedSubarray(int[] nums)
    {
        Stack<Integer> stack = new Stack<Integer>();
        int n = nums.length;
        int left = n, right = 0;
        for(int i=0; i<n; i++)
        {
            while(!stack.isEmpty() && nums[stack.peek()]>nums[i])
            {
                left = Math.min(left, stack.pop());
            }
            stack.push(i);
        }
        stack.clear();
        for(int i=n-1; i>=0; i--)
        {
            while(!stack.isEmpty() && nums[stack.peek()]<nums[i])
            {
                right = Math.max(right, stack.pop());
            }
            stack.push(i);
        }
        
        return left-right > 0 ? 0 : right-left+1;
    }
}
```

#### 方法3改进1：不使用额外空间[Accepted]
思想：在未排序的子数组中，最小元素的正确位置确定所需的左边界，最大元素的正确位置确定所需的右边界。

首先，需要确定正确排序的数组何时出错，通过从数组左端观察上升斜率来判断。每当斜率下降时，未排序的数组肯定开始了。这样扫描整个数组，知道数组末尾，找到的最小元素min。类似地反方向扫描数组，当斜率上升时开始寻找最大元素，直到到达数组的开始，找出max。

然后，遍历nums，并通过min和max元素与其他数组元素进行比较，来确定min和max的正确位置。对于min的正确位置，已知nums的初始部分已经被排序了，因此，需要找到比min更大的第一个元素。max类似。

```java
//java
class Solution {
    public int findUnsortedSubarray(int[] nums)
    {
        int n = nums.length;
        int min = Integer.MAX_VALUE, max = Integer.MIN_VALUE;

        for(int i=1; i<n; i++)
        {
            if(nums[i] < nums[i-1])
                min = Math.min(min, nums[i]);
        }

        for(int i=n-2; i>=0; i--)
        {
            if(nums[i] > nums[i+1])
                max = Math.max(max, nums[i]);
        }
        
        int left, right;
        for(left=0; left<n; left++)
        {
            if(min < nums[left])
                break;
        }
        for(right=n-1; right>=0; right--)
        {
            if(max>nums[right])
                break;
        }
        
        return left - right > 0 ? 0 : right - left + 1;
    }
}
```
