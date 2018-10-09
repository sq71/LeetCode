## Intuition
高斯公式。
```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) 
    {
        int sum = 0;
        int n;
        for(int i : nums)
            sum += i;
        n = (nums.size() + 1) * nums.size() / 2;
        return n-sum; 
    }
};
```
