- nullptr是c++11中的关键字，表示空指针。书中的例子经常看到判断函数的参数是否为空指针。
- 引用和指针做参数的区别？功能差不多，但是**优先用引用**。引用本身只是一个别名，本身不占内存，但是指针首先是变量，本身是要占内存的。引用作为形参也更方便寻址。



## 常用函数

`sort()`  参数是两个指针，默认升序。

`swap()`   

`sprintf( char *buffer, const char *format [, argument] … )` 打印数据到一个字符串变量。

`void qsort(void*base,size_t num,size_t width,int(__cdecl*compare)(const void*,const void*))`  base需要排序的目标数组开始地址， num目标数组元素个数，width每个元素长度， compare比较函数。compare函数的参数类型是空指针，需要自己转换类型。排序后的数组，能够满足使compare函数返回true。

`strcat()`  拼接两个字符串

`strcpy()` 拷贝字符串

`strcmp()` 相当于两个字符串做减法，相等返回0，str1小于str2，返回负数。 str1大于str2，  返回正数。

`vector.end() - 1` 才是vector末尾元素的指针



## 字符串处理

ascii码为0的字符是'\0'

`string s` 添加字符 `s.append(c, 3)` 把字符串c的前3个字符添加到s末尾， `s.append(c)` 把字符串c添加到s末尾。



## STL相关

size()的时间复杂度是O(1)还是O(n) 取决于STL的版本，和编译器有关，比如vc6中的size是O(1)， gcc中的size是O(n)。

复制一个容器来初始化`vector<int> v(v_old)`

