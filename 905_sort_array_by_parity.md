## 思路
#### 方法1：

先遍历一遍vector，把偶数存到res，把奇数存到temp，再遍历temp把元素都push_back到res。

Runtime: 40 ms
```
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& A) 
	{
		vector<int> res;
		vector<int> temp;
		for(int i=0; i<A.size(); ++i)
		{
			if(A[i]%2 == 0)
				res.push_back(A[i]);
			else
				temp.push_back(A[i]);
		}
		
		for(int i=0; i<temp.size(); ++i)
			res.push_back(temp[i]);
		
		return res;
    }
};
```

下面方法更快一点：

Runtime: 28 ms
```
class Solution {
public:
    vector<int> sortArrayByParity(vector<int>& a)
    {
        
        vector<int> res;
        for(int i=0; i<a.size(); ++i)
        {
            if(a[i]%2 == 0)
            {
                res.push_back(a[i]);
            }
        }
        for(int j=0; j<a.size(); ++j)
        {
            if(a[j] % 2 != 0)
                res.push_back(a[j]);
        }
        return res;
    }
};
```

#### 方法2：

设置两个索引，分别从A的前后两端往中间移动，找到第一个奇数和偶数，交换，直到索引相遇。

Runtime: 52 ms

不重写swap函数 Runtime：32 ms

```
class Solution {
public:
    void swap(int &a,int &b)
    {
        int temp = a;
		a = b;
	    b = temp;
    }
    vector<int> sortArrayByParity(vector<int>& A) 
    {
        int i = 0,j = A.size() - 1;
        while(i < j)
        {
            while(A[i] % 2 == 0)
			    i++;
			while(A[j] % 2 != 0)
		    	j--;
            if(i < j)
            {
                swap(A[i++],A[j--]);
            )
        }
        return A;
    }
};

```

