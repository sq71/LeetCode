## 思路
代码如下：
```
class Solution {
public:
    int maxProfit(vector<int>& prices) 
    {
        int res = 0;
        for(int i=1; i<prices.size(); ++i)
        {
            if(prices[i-1] < prices[i])
                res += (prices[i] - prices[i-1]);
        }
        return res;
    }
};

```
问题：为什么for(int i=1; i<prices.size(); ++i)替换成for(int i=0; i<prices.size()-1; ++i)不能通过？


