## 思路

这道题是非常实用的，比如搜索引擎的自动补全

和set相比，Trie前缀树多了一个`startsWith()`方法。

直接的思路，开一个数据set，再开一个前缀set，再insert时，把前i个字符都insert到前缀set中。这种方法空间开销太大了。但是leetcode上也过了。

**正确的思路**

设计一个树结构，树的第i层表示字符串中的第i个字符的取值，也就是每个节点有26个子树（26个树节点组成的数组）。每个子树是否存在，表示是否出现过第i个字符为 对应字符 的情况。

1）向前缀树中插入字符串：遍历字符串中的每个字符，查找当前前缀树的第i个字符对应的节点上，是否有子树，如果是空（说明没有子树），就新创建一个前缀树节点，连接到当前节点的 26个子树中对应的那一个子树上（这个子树之前是没有的）。

2）在前缀树中查找字符串：遍历字符串中的每个字符，判断第i个位置上的字符是否有子树，如果有子树，说明截止到字符串的第i个字符。**但是我们还需要区分 完整的字符串 和 前缀**， 所以对每个节点需要加一个标记，表示当前子串 是否出现过完整的字符串，还是只是一个前缀。**在插入字符串时设置这个标记。**

3）在前缀树中查找前缀： 和查找字符串类似，而且不需要判断是不是一个完整的字符串。

## 代码

开两个set。

```c++
class Trie {
public:
    /** Initialize your data structure here. */
    unordered_set<string> data;
    unordered_set<string> trie;
    Trie() {
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        data.insert(word);
        for(int i=1;i<=word.size();i++){
            trie.insert(word.substr(0,i));
        }
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        return data.find(word)!=data.end();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        return trie.find(prefix)!=trie.end();
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

