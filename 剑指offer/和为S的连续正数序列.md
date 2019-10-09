## 思路

感觉可以用动态规划。

首先数字的范围是 1 到 sum/2。

考虑连续正数的规律，连续正数是一个差为1的等差数列，可以写出其和的公式，和起始值、元素数量有关。并且起始值和元素数量都是正数。

1) 可以遍历元素数量，然后用公式反求a1, 然后判断a1是不是整数。复杂度是O(n)。 但其实不太好判断a1是不是整数。

2) 应该能用双指针，但是范围不一定是一直缩小的，因为连续序列的长度不确定。



**正确的思路:**

还是用双指针，只不过判断条件不一样了。 并且两个指针并不是从两端向中间移动。而是**两个指针都是从小变大。** 直到较小的值，大于sum/2，因为此时较大的值也大于sum/2,  两个指针再变大，其之间的数的和，一定是大于sum的。



## 代码

```c++
class Solution {
public:
    vector<vector<int> > FindContinuousSequence(int sum) {
        vector< vector<int> > res;
        if(sum <= 2)
            return res;
        
        int start = 1;
        int end = 2;
        int tSum = start + end;
        
        while(  start <= sum/2 )
        {
            if(tSum == sum){
                vector<int> tmp;
                for( int i=start;i<=end;i++ )
                {
                    tmp.push_back(i);
                }
                res.push_back(tmp);
            }
            
            if(tSum < sum)
            {
                end+=1;
            }
            if(tSum >= sum)
            {
                 start+=1;
            }
            
            tSum = sumSeries(start, end);
        }
        
        return res;        
    }
    
    int sumSeries(int s1, int s2)
    {
        // 求两个数之间的数的和
        int tmp1 = s2-s1+1;
        int tmp2 = s1+s2;
        
        return tmp1*tmp2/2;
    }
    
};
```

