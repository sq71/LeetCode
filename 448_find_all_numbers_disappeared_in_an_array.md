## 思路
问题关键是向量中每一个元素都是正数且取值范围为[1,n]，即每个元素的值的大小与向量的坐标是一一对应的。所以有如下解法：

#### 方法1：
```
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) 
    {
        for(int i=0; i<nums.size(); ++i)
        {
            int index = abs(nums[i])-1;
            nums[index] = nums[index]>0 ? -nums[index] : nums[index];
        }
        
        vector<int> res;
        
        for(int i=0; i<nums.size(); ++i)
        {
            if(nums[i] > 0)
                res.push_back(i+1);
        }
        
        return res;
    }
};
```
因为一一对应，可以把与每个元素的值相等（其实是减1）的索引所对应的元素，取其绝对值的相反数。
这样最后可以根据某个位置的元素值为正，推断出向量中没有相应的（位置+1的）元素出现过。

#### 方法2：
类似方法1, 如果一个位置上的元素与该元素对应索引上的元素值，不相等，则互换两者的值，循环，直至相等。注意要有循环。
可理解为：“本位置的元素应该放到对应的地方上”。
```


class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) 
    {
        int i=0;
        while(i < nums.size())
        {
            if(nums[i] != nums[nums[i]-1])
                swap(nums[i], nums[nums[i]-1]);
            else
                ++i;
        }
        
        vector<int> res;
        
        for(int i=0; i<nums.size(); ++i)
        {
            if(i+1 != nums[i])
                res.push_back(i+1);
        }
        
        return res;
    }
};
```
