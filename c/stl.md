# stl

---
## set

- 遍历

```c++
set<int> s;
set<int>::iterator it = s.begin();
for (; it != s.end(); ++it) {
    std::cout<< *it <<std::endl;
}
```

---
## vector
> stl 的 map，vector 实现原理，内存管理，排序，优缺点。

| 接口     | 解析                                                                                                                                        |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| capacity | 当前容器容量，capacity 增长的策略不同的平台下，情况不一样，mac 和 centos 就不一样。                                                         |
| size     | 当前数据长度                                                                                                                                |
| reserve  | 根据目标数据告诉容器应该预留多少个元素的存储空间，影响 capacity                                                                             |
| resize   | 调整当前数据大小，对数据有初始化功能；小于那么 capc 不变，大于capc 要改变，当resize 大小有改变且大于当前 capacity，那么 capacity 会加倍增长 |

vector 容器自增长，数组内存都是连续的，为了增加数组的使用效率，会对内存进行预分配。
vector 不得不重新分配新的内存时以**加倍当前容量**的分配策略实现重新分配
==> 因为动态内存分配数组，数组内部会根据内容输入的容量增长，不断重新分配内存，如果数组要连续输入数量比较多的内容，可以通过 reserve （或者 resize）接口为目标数据预分配足够的空间，这样，数组在操作过程中，就不会频繁进行内存的重新分配，导致效率低下。

```c++
#include <iostream>
#include <vector>

const int g_array_len = 612;
using namespace std;

void traversal(int len) {
    vector<int> v;
    for (int i = 0; i < len; i++) {
        v.push_back(i);
        printf("data: %d, size: %lu, capc: %lu\n", v[i], v.size(), v.capacity());
    }
}

void reserve(int len) {
    vector<int> v;
    v.reserve(len);
    for (int i = 0; i < len; i++) {
        v.push_back(i);
        printf("data: %d, size: %lu, capc: %lu\n", v[i], v.size(), v.capacity());
    }
}

void resize(int len) {
    vector<int> v;
    v.reserve(len);
    printf("vector size: %lu, capc: %lu\n", v.size(), v.capacity());
    v.resize(len+1, 5);
    printf("vector size: %lu, capc: %lu\n", v.size(), v.capacity());
    printf("v[%d] = %d\n", len+1, v[len+1]);
}

int main() {
    // 可以通过遍历数据，观察 vector 内部的内存分配情况。
    // traversal(g_array_len);

    // 预分配容器容量，观察容器内部的内存分配情况。
    // reserve(g_array_len);

    // 预分配容器容量，目标数据超出容量，观察容器内部的内存分配情况。
    // reserve(g_array_len + 1);

    // 
    resize(g_array_len);
    return 0;
}
```

---
## 参考
[文档](https://zh.cppreference.com/w/cpp/container/set/begin)
[多线程](https://www.jianshu.com/u/88ad4f76eb79)
[c++ 官网](http://www.cplusplus.com/)