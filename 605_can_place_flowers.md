# java
从前往后遍历数组，对于其中值为零的元素，若其左右相邻元素的值也为0，则符合题意。注意数组首尾两端的特例元素。

```java
//java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) 
    {
        for(int i=0; i<flowerbed.length; i++)
        {
            if(flowerbed[i]==0 && (i==0 || flowerbed[i-1]==0) && (i==flowerbed.length-1 || flowerbed[i+1]==0))
            {
                flowerbed[i] = 1;
                n--;
            }
        }

        return n<=0 ? true : false;
    }
}
```
