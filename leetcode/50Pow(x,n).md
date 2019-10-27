## 思路

输入x是double， n是有符号数，如果是负数，就先取绝对值，之后在取倒数。

x的n次方，n的范围是32位有符号数。暴力可能要循环20亿次。肯定是不行的。

做了两数相除那道题，知道这种可以类别用位运算来做。因为x分解成2^n项的累加，然后取n次方，是不等于x^n的，所以自然考虑把n分解。

假设 n = 14(二进制是1110), 那么有

$x^n = x^{2^3*1+2^2*1+2^1*1+2^0*0} = x^{2^3}*x^{2^2}*x^{2^1}*x^{0} $

这种方法的时间复杂度是O(logn). 这种方法其实和常规的二分类似，不过感觉用位运算更容易理解。



## 代码

暴力,  时间复杂度是O(logn) 超时，但是逻辑应该没问题

```c++
class Solution {
public:
    double myPow(double x, int n) {
        if(n==0)
            return 1;
        
        double ret=1;
        bool mSign = (n<0); // n是否有符号
        bool flag = (n==INT_MIN); // n==INT_MIN时，取绝对值会有问题
        if(flag) n+=1; // 如果n是INT_MIN, n就先加1, 避免对INT_MIN取绝对值时溢出
         
        n = abs(n);

        while(n>0){
            n-=1;
            ret*=x;
        } 

        if(flag){
            ret*=x;
        }

        return mSign?1/ret:ret;
    }
};
```



快速幂, 时间复杂度O(logn)

```c++
class Solution {
public:
    double myPow(double x, int n) {
        if(n==0)
            return 1;
        
        double ret=1;
        bool mSign = (n<0); // n是否有符号
        bool flag = (n==INT_MIN); // n==INT_MIN时，取绝对值会有问题
        if(flag) n+=1; // 如果n是INT_MIN, n就先加1, 避免对INT_MIN取绝对值时溢出
         
        n = abs(n);

        int mi2=0; // 2^mi2 = 1<<mi2
        double tmp=x; // 保存x^(2^mi2)
        while(n>0){
            if(n&0x1)
                ret=ret*tmp;
            tmp = tmp*tmp;
            n = n>>1;
            mi2+=1;
        } 

        if(flag){
            ret*=x;
        }

        return mSign?1/ret:ret;
    }
};
```



