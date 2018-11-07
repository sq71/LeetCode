## 思路
这道题要求从有序数组中去除重复项，可以使用两个指针。

#### 原始代码
```java
// java
class Solution {
    public int removeDuplicates(int[] nums) 
    {
        int n=nums.length;
        int i=0, j=0;
        while(j<n)
        {
            while(j<n && nums[j]==nums[i]) //这里注意：为了防止数组越界访问，第二个while循环里面必须也要有且先有j<n的限定。
                ++j;
            if(j<n)
                nums[++i] = nums[j];
        }
        return i+1;
    }
}
```
#### 重新整理代码
用快慢指针来记录遍历的坐标，最开始时两个指针同时指向nums[0]，
若两个指针所指数字相同，则快指针向前走一步；若不同，则两个指针同时向前走一步。
当快指针走完整个数组后，慢指针当前的坐标加1，即为数组中不同数字的个数。

使用while循环的代码：
```java
//java
class Solution {
    public int removeDuplicates(int[] nums) 
    {
        int i = 0, j = 0, n = length;
        while (j < n) 
        {
            if(nums[i] == nums[j]) 
                j++;
            else 
                nums[++i] = nums[j++];
        }
        return i+1;
    }
};
```
使用for循环的代码：
```java
//java
class Solution {
    public int removeDuplicates(int[] nums) 
    {
        int i = 0, n = nums.length;
        for(int j=0; j<n; j++)
        {
            if(nums[j] != nums[i]) 
                nums[++i] = nums[j];
        }
        return i+1;
    }
};
```
