## 思路
用map来做。先找出数组中所有值出现的次数，再求出数组的度。
对于所有出现次数与数组的度相同的值，计算它们最早出现与最后出现的位置间的距离，距离最小值即为所求。

```
class Solution {
public:
    int findShortestSubArray(vector<int>& nums) 
    {
        map<int, vector<int>> mp;
        for(int i=0; i<nums.size(); ++i)
        {
            mp[nums[i]].push_back(i);
        }
        
        int degree = 0;
        int maxd = 0;
        
        for(auto it=mp.begin(); it!=mp.end(); ++it)
        {
            maxd = max(maxd, int(it->second.size()));
        }
        
        int res = 50000;
        
        for(auto it=mp.begin(); it != mp.end(); ++it)
        {
            if (it->second.size() == maxd)
            {
                res = min(res, int(it->second.back()) - int(it->second[0]) + 1);
            }
        }
        
        return res;
    }
};
```
