## 思路
从左往右，把非0的元素依次移动到左端。
```
class Solution {
public:
    void moveZeroes(vector<int>& nums) 
    {
        int j=0;
        for(int i=0; i<nums.size(); ++i)
        {
            if(nums[i] != 0)
            {
            //或者这里直接用swap函数交换两者的值，可以略去后面循环赋值为0的操作
                nums[j] = nums[i];
                ++j;
            }
        }
        for(; j<nums.size(); ++j)
            nums[j] = 0;
    }
};
```

