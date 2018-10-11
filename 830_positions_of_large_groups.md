## Intuition
如下。
```c++
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string S) 
    {
        vector<vector<int>> res;
        int n=1;
        for(int i=1; i<S.size();)
        {
            if(S[i] == S[i-1])
            {
                n++;
                i++;
            }
            else
            {
                if(n >= 3)
                    res.push_back({i-n, i-1});
                n=1;
                i++;
            }
            
                        
            if(i == S.size() && n >=3)
                res.push_back({i-n, i-1});

        }
        return res;
    }
};
```
#### 改进
上述代码中索引从1开始，改为从0，并且省略变量n：
```C++
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string S) 
    {
        vector<vector<int>> res;
        int i=0,j=0;
        while(i<S.size())
        {
            while(i<S.size() && S[i]==S[j])
            {
                j++;
            }
            if(j-i >= 3)
                res.push_back({i, j-1});
            i = j;
        }
        return res;
    }
};

```
下面的代码错在哪里？
```c++
class Solution {
public:
    vector<vector<int>> largeGroupPositions(string S) 
    {
        vector<vector<int>> res;
        int n=1;
        int i=1;
        while(i<S.size())
        {
            while(i<S.size() && S[i]==S[i-1])
            {
                i++;
                n++;
            }
            if(n>=3)
                res.push_back({i-n, i-1});
            n=1;
        }
        return res;
    }
};
```
