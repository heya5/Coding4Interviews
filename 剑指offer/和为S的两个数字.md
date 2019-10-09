## 思路

要求返回所有和为s的两个数字，其中乘积最小的。根据均值不等式，和相等时，两个数字相差越大，成绩越大。两个数字相等时，乘积最小。

1) 暴力的复杂度是O(n^2)



**更好的思路:** 

2) 可以用双指针快速缩小查找范围。（因为数组是有序的，对有序的数组，要考虑，能不能用二分，双指针）

首先两个指针分别指向数组的首尾元素，此时两个元素和如果小于sum，就让前面一个指针向后移动； 如果元素和大于sum，就让后面一个指针向前移动。这样找到的第一个和为sum的两个元素，就是乘积最小的元素。

如何找乘积最大的两个数字? 两个指针从数组的中间位置向两边走，第一个和为sum的两个元素，就是乘积最大的。



**出错的地方:**

1) 循环时，前面的指针要大于后面的指针，如果后面的指针移动到前面，要退出循环。

2) `vector.end()-1` 才是末尾元素的指针



## 代码

```c++
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> array,int sum) {
        vector<int> res;
        if( array.empty() )
            return res;
        
        vector<int>::iterator iter1 = array.begin();
        vector<int>::iterator iter2 = array.end()-1;
        int tSum = *iter1 + (*iter2);
        
        while( (tSum!=sum) && (iter1<iter2) ){
            if(tSum < sum)
                iter1+=1;
            else
                iter2-=1;
            tSum = *iter1 + (*iter2);
        }
        
        if(tSum==sum){
            res.push_back(*iter1);
            res.push_back(*iter2);
        }
        return res;
    }
};
```

