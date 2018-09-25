## 思路
排序，再判断相邻两个数是否相等。
```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) 
    {
        sort(nums.begin(), nums.end());
        for(int i=1; i<nums.size(); ++i)
        {
            if(nums[i]-nums[i-1] == 0)
                return true;
        }
        
        return false;
    }
};
```

#### 方法2 
使用set

```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) 
    {
        set<int> s(nums.begin(), nums.end());
        return nums.size() != s.size();
    }
};
```

#### 方法3
哈希表

