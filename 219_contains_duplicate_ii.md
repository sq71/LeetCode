# Java
## 初始代码[Time Limit Exceeded]
使用两层循环，判断每一个数i左右k个数内是否存在与其相同的数，若存在则为true。但是此方法超时。
```java
// java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) 
    {
        int n =nums.length;
        for(int i=0; i<n; i++)
        {
            int a = i-k, b = i+k;
            int cnt = 0;
            if(i+k >= n)    b = n-1;
            if(i-k <= 0)    a = 0;
            for(int j=a; j<=b; j++)
            {
                if(nums[j] == nums[i])
                    cnt++;
                if(cnt == 2)
                    return true;
            }
        }
        
        return false;
    }
}
```

## 改进1 [Time Limit Exceeded]
依然使用两层循环，只是遍历整个数组，判断该数往后数k个数内是否存在与之相同的数。仍然超时，看来使用两层循环是不行了。
```java
// java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) 
    {
        int n =nums.length;
        for(int i=0; i<n; i++)
        {
            for(int j=1; i+j<n && j<=k; j++)
                if(nums[i+j] == nums[i])
                    return true;
        }
        return false;
    }
}
```

## 方法1：HashMap [Accepted]
```java
//Java
class Solution 
{
    public boolean containsNearbyDuplicate(int[] nums, int k) 
    {
        int n = nums.length; 
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for(int i=0; i<n; i++)
        {
            if(map.containsKey(nums[i]))
                if(i - map.get(nums[i]) <= k)
                    return true;
            
            map.put(nums[i], i);
        }      
        return false;
    }
}
```
## 方法2：HashSet (sliding window）[accepted]
```java
// java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) 
    {
        Set<Integer> set = new HashSet<Integer>();
        for(int i = 0; i < nums.length; i++)
        {
            if(i > k) 
                set.remove(nums[i-k-1]);
            if(!set.add(nums[i])) 
                return true;
        }
        
        return false;
    }
}
```
---
# C++

