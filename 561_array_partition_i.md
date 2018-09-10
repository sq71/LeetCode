## 思路
显然是把数组排序，从小到大每隔一个数进行求和。

## 方法一
直接想到的方法：使用sort函数排序
```
class Solution {
public:
    int arrayPairSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int sum = 0;
        for(int i=0; i<nums.size(); i+=2)
            sum+=nums[i];
        return sum;
    }
};
```
因为使用了sort函数，所以时间复杂度为 _O(nlogn)_ 。

## 方法二
在讨论区发现一种 _O(n)_ 的方法：
```
int arrayPairSum(vector<int>& nums) {
    vector<int> v(20001, 0);
    for(int n: nums) v[n + 10000]++;
    int res = 0;
    bool flag = true;
    int i = 0;
    while(i < 20001){
        if(v[i] >= 1){
            res = flag? res + i - 10000 : res;
            flag = flag ^ 1; // flag = !flag
            v[i]--;
        }
        if(v[i] == 0) i++;
    }
    return res;
}
```
此方法建立了一个哈希表。（有人说是桶排序？）
