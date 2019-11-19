## 思路

暴力思路，用hash map统计每个元素的出现次数，然后把hash map的key和value拷贝到一个vector里，按照value排序，取前k个key。时间复杂度O(nlogn)。

能否先对数组排个序？没思路。

**更好的方法**

我的思路也可以过，时间复杂度是O(nlogn) 。 但是题目要求由于时间复杂度优于O(nlogn), 可以用堆排序来做。堆排序后面再针对性看。



## 代码

时间复杂度O(nlogn)

```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        vector<int> ret;
        unordered_map<int, int> hash;
        for(auto v:nums){
            hash[v]+=1;
        }
        vector< pair<int, int> > tmpMap;
        for(auto v:hash){
            // cout<<v.second<<endl;
            tmpMap.push_back(v);
        }
        sort(tmpMap.begin(), tmpMap.end(), myCmp);

        for(int i=0;i<k;i++){
            ret.push_back(tmpMap[i].first);
        }

        return ret;
    }

    static bool myCmp(const pair<int,int>& a, const pair<int, int>& b){
        if(a.second>b.second) return true;
        else return false;
    }
};
```

