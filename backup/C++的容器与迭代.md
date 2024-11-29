#C++中的容器与迭代器
首先我们提出一个问题：容器与迭代是什么？

##容器是什么？
在我看来容器就是“容纳一定内容的空间”。比如数组就是一个容器，一个`int a[10]`数组，可以容纳10个整型数字。
值得注意的是，容器依据其中是否重复，划分为不同形式：

如数组类型，其中元素可以重复。
如set类型，其中元素不能重复。我们先看看set类型是什么。

###一个有序、不含重复元素的容器——set
具有以下特点：

- 元素不重复
- 自动排序
- 查找很快

```cpp
#include <set>//注意include相应文件
#include <iostream>
using namespace std;

int main() 
{
    // 创建set
    set<int> s1;                     // 空set
    set<int> s2 = {3, 1, 4, 1, 5};  // 初始化，注意1只会保存一次
    
    // 插入元素
    s1.insert(10);
    s1.insert(20);
    
    // 删除元素
    s1.erase(10);
}
```

###键值对——map
先看例子：
```
#include <map>
#include <string>
using namespace std;

int main()
 {
    // 键值对示例：
    // 键(Key)      值(Value)
    // "张三"  →    95        // 学生姓名是键，分数是值
    // "李四"  →    88
    // "王五"  →    90
    
    map<string, int> scores;  // 声明map，string类型是键，int类型是值
    
    // 插入键值对
    scores["张三"] = 95;
    
    // 通过键访问值
    cout << scores["张三"] << endl;  // 输出95
    
    // 键必须唯一，值可以重复
    scores["张三"] = 96;  // 更新张三的分数
    scores["李四"] = 95;  // 可以和张三的分数相同
    
    // 实际应用场景
    map<string, string> dict;     // 字典：单词 → 释义
    map<int, string> idToName;    // ID映射：工号 → 姓名
    map<string, vector<int>> studentScores;  // 复杂映射：学生 → 多个成绩
}
```
这就是说通过Key直接找到值。但是键确定了就不能轻易修改，除非把该键值对删掉，重新找一个键对应该值。
---
##迭代器是什么？
迭代器就像一个指针，用来指向容器中的元素（注意数组与指针的关系）。它提供了访问容器元素的方法。
```cpp
#include <vector>
#include <iostream>
using namespace std;

int main() {
    vector<int> nums = {1, 2, 3, 4, 5};
    
    // 指针操作
    int arr[] = {1, 2, 3, 4, 5};
    int* p = arr;
    cout << *p << endl;      // 解引用
    p++;                     // 移动到下一个元素
    
    // 迭代器操作（类似指针）
    auto it = nums.begin();
    cout << *it << endl;     // 解引用
    it++;                    // 移动到下一个元素
    
    // 迭代器的额外功能
    vector<int>::iterator it2 = nums.begin();
    it2 += 2;               // 可以跳过多个元素（随机访问迭代器支持）
    cout << it2[2] << endl; // 支持下标访问（随机访问迭代器支持）
    
    // 迭代器的安全性
    nums.push_back(6);      // 添加元素可能导致迭代器失效
    // it = nums.begin();   // 需要重新获取迭代器
}
```
---
##写在最后——容器中元素的查找
有一些**现有的函数**可以直接使用。
#####比如find函数：
```
#include <vector>
#include <map>
#include <algorithm>  // 包含find函数
using namespace std;

int main() {
    // 1. 在map中使用find
    map<string, int> scores = {
        {"张三", 95},
        {"李四", 88},
        {"王五", 90}
    };
    
    // map的find方法
    auto it = scores.find("张三");
    if(it != scores.end()) {
        cout << "找到了：" << it->first << " " << it->second << endl;
    }
    
    // 2. 在vector中使用find
    vector<int> nums = {1, 2, 3, 4, 5};
    
    // 算法find
    auto result = find(nums.begin(), nums.end(), 3);
    if(result != nums.end()) {
        cout << "找到了：" << *result << endl;
    }
}

```
