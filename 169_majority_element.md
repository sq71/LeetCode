## 思路
因为majority element 的个数more than⌊ n/2 ⌋ times，可知把向量排序后，中间位置的数一定为所求。
```
class Solution {
public:
    int majorityElement(vector<int>& nums) 
    {
        sort(nums.begin(), nums.end());
        return nums[nums.size()/2];
    }
};
```
