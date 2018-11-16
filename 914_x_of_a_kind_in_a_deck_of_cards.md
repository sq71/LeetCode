# Java
1. 统计每个数出现的次数；2.计算它们的最大公约数gcd，大于2则符合题意。

```java
//java
class Solution {
    public boolean hasGroupsSizeX(int[] deck) 
    {
        HashMap<Integer, Integer> map = new HashMap<>();
        for(int x : deck)
        {
            map.put(x, map.getOrDefault(x , 0)+1);
        }
        
        int g = 0;
        for(int x : map.values())
        {
            g = gcd(x, g);
        }
        
        return g > 1 ? true : false;
    }
    
    int gcd(int x, int y)
    {
        return y == 0 ? x : gcd(y, x%y); 
    }
}
```
