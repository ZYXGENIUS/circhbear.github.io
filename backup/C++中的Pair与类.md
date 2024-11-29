#C++中Pair与类
Pair是将两个数据合成一个数据的模板类。在utility头文件中。
它的介绍如下：
```cpp
    // 创建pair的几种方法
    pair<string, int> p1;                    // 创建了一个名叫p1的pair，里面第一个元素是string，另一个元素是int
```
如果需要访问（下面以赋值为例）：
```cpp
p1.first = "大学生";
p1.second = 18；
```
可以看出Pair的使用方法和类很相似。实际上，Pair是一个类的模板，这个类中只有两个成员。
不妨这样看待：
```cpp
class MyPair
 {
public:
    int first;//第一个是first，第二个是second，这是固定的。
    float second;//
    
    MyPair() : first(), second() {}
    MyPair(const T1& x, const T2& y) : first(x), second(y) {}
};
```
---

