## 思路
假定数组为Monotonic，先比较数组首尾元素大小判断数组是递增的还是递减的，对于每一种情况，找到反例则为false，找不到则为true。

Runtime: 56 ms
```
class Solution {
public:
    bool isMonotonic(vector<int>& A) 
    {
        int size = A.size();
        if(A[size-1] <= A[0])
        {
            for(int i=0; i<size-1; ++i)
            {
                if(A[i] < A[i+1])
                    return false;
            }
        }
        
        else if(A[size-1] > A[0])
        {
            for(int i=0; i<size-1; ++i)
            {
                if(A[i] > A[i+1])
                    return false;
            }
        }
        
        return true;
        
    }
};
```

（提交的代码中，很多使用了Lambda表达式的代码用时很短。）
