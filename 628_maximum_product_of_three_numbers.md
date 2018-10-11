## intuition
注意考虑有负数存在的情况，所以所求最大值一定在`max1*max2*max3`和`min1*min2*max3`中间。

```C++
class Solution {
public:
    int maximumProduct(vector<int>& nums) 
    {
        int max1 = -1001, max2 = -1001, max3 = -1001;
        int min1 = 1001, min2 = 1001;
        for(int x : nums)
        {   //找出最大的三个数 max1 < max2 < max3
            if(x > max3)
            {
                max1 = max2;
                max2 = max3;
                max3 = x;
            }
            else if(x > max2)
            {
                max1 = max2;
                max2 = x;
            }
            else if(x > max1)
                max1 = x;
        
                
        //找出最小的两个数 min2 < min1
            if(x < min1)
            {
                min2 = min1;
                min1 = x;
            }
            else if(x < min2)
            {
                min2 = x;
            }
        }
        
        return max(max1*max2*max3, min1*min2*max3);
        
        
    }
};
```
