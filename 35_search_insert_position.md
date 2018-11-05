二分查找。

## Java
```java
class Solution {
    public int searchInsert(int[] nums, int target) 
    {
        int i=0, j=nums.length-1;
        while(i <= j)
        {
            int mid = (i+j)/2;
            if(target == nums[mid])
                return mid;
            else if(target < nums[mid])
                j = mid-1;
            else
                i = mid+1;
        }
        
        return i;
    }
    
}
```
返回的是i。
