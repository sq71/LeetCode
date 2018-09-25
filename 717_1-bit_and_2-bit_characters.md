## 思路
1.向量长为1时，true；

2.向量长为2时，设置索引i=0，当bits[i]值为1时，i+=2；当值为0时，i++。判断最后i会不会指向最后一个数，会则为true，不会为false。

```
class Solution {
public:
    bool isOneBitCharacter(vector<int>& bits) 
    {
        int i=0;
        
        if(bits.size() == 1)
            return true;
        
        while(true)
        {
            if(bits[i] == 1)
                i +=2;
            else
                ++i;
            
            if(i == bits.size()-1)
                return true;
            if(i == bits.size())
                return false;
        }
    }
};
```
