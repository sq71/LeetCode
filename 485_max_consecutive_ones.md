## 思路

我写的代码：
```class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) 
    {
        nums.push_back(0);
        
        int res = 0;
        
        for(int i=0; i<nums.size()-1; ++i)
        {
            int temp = 0;
            if(nums[i] == 1)
            {
                temp++;
                while(nums[i+1] != 0)
                {
                    temp++;
                    i++;
                }
                res = (temp > res ? temp:res);
            } 
        }
        return res;
    }
};

```

简化的代码: 
```
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums)
    {
        int max=0, count=0;
        for(int n : nums)
        {
            if(n == 1) 
                count++;
            else 
                count = 0;
            
            max = (max < count ? count : max);
        }
        return max;
    }
};
```
把if(n == 1)替换成if(n & 1)会快一点：

Runtime: 24 ms -> 20 ms
