# Java
## 思路
使用两个指针i、j，分别从两个数组nums1、nums2的非零末端往前遍历，比较两指针所之的元素大小，并把较大元素插入数组末端。 
需要注意若num1先遍历完，需要把剩下的nums2中元素插入到nums1中。

```java
//java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) 
    {
        int i=m-1, j=n-1;
        int k = m+n-1;
        while(i>-1 && j>-1)
        {
            nums1[k--] = nums1[i] > nums2[j] ? nums1[i--] : nums2[j--];
        }
        
        while(j>-1)
        {
            nums1[k--] = nums2[j--];
        }
    }
}
```
