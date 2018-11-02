## Intuition
两层循环。

从第二行开始，每一行中除了第一个和最后一个元素，其它元素计算方式为` v(i)(j) = v(i-1)(j-1)+v(i-1)(j)`。

## Java
```java
class Solution {
    public List<List<Integer>> generate(int numRows) 
    {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        
        if(numRows == 0) //不要也行，会被下面的for循环过滤掉
            return res;
        
        for(int i=0; i<numRows; i++)
        {
            List<Integer> row = new ArrayList<Integer>();
            for(int j=0; j<i+1; j++)
            {
                if(j==0 || j==i)
                    row.add(1);
                else 
                    row.add(res.get(i-1).get(j-1) + res.get(i-1).get(j));
            }
            
            res.add(row);
        }
        
        return res;
    }
}
```
