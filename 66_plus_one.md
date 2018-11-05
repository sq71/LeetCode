## 思路
从最后一位向前看起，若为9，则变0（+1）；若不为9，则本位加1，返回；若所有位都为9，则创建比原数组多一位的新数组，新数组第一位赋值为1。

#### Java
```java
class Solution {
    public int[] plusOne(int[] digits) 
    {
        int n = digits.length;
        for(int i=n-1; i>=0; i--)
        {
            if(digits[i] == 9)
                digits[i] = 0;
            else
            {
                digits[i]++;
                return digits;
            }
        }
        int[] res = new int[n+1];
        res[0] = 1;
        return res;
    }
}
```

#### C++
```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) 
    {
        int n = digits.size();
        for(int i=n-1; i>=0; i--)
        {
            if(digits[i] == 9)
                digits[i] = 0;
            else
            {
                digits[i]++;
                return digits;
            }
        }
        
        digits[0] = 1;
        digits.push_back(0);
        
        return digits;
    }
};
```
