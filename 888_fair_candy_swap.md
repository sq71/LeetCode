## 思路
先计算出需要从A转移至B的量（正或负），再对于A中每一个元素，遍历B寻找其中相差为temp的元素。

```
class Solution {
public:
    vector<int> fairCandySwap(vector<int>& A, vector<int>& B) 
    {
        int sum_a=0, sum_b=0;
        int temp;
        
        for(int a : A)
            sum_a += a;
        for(int b : B)
            sum_b += b;
        
        temp = (sum_a - sum_b) / 2;
        
        for(int a : A)
            for(int b : B)
                if(a-b == temp)
                    return {a, b};
    }
};
```
发现：使用for(a:A)比使用for(; ;)要慢。


STL中有求和算法accumulate：

int sum =  accumulate(vec.cbegin(), vec.cend(), 0);

#### 方法2：
使用set

Runtime: 76 ms
```
class Solution {
public:
    vector<int> fairCandySwap(vector<int>& A, vector<int>& B) 
    {
        int sum_a=0, sum_b=0;
        int temp;
        
        for(int a : A)
            sum_a += a;
        for(int b : B)
            sum_b += b;
        
        temp = (sum_a - sum_b) / 2;
        
        set<int> bSet;
        
        for(int b:B)
            bSet.insert(b);
        
        for(int a:A)
        {
            int setVal = a-temp;
            if(bSet.find(setVal) != bSet.end())
                return {a, setVal};
        }
    }
};
```

#### 方法2.1:
使用unordered_set

Runtime: 80 ms

