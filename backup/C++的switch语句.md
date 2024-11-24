# 循环控制之switch

**switch**语句相对于**for**语句、**while**使用相对较少，写这篇博客的原因是因为刚刚做题就做错了，现在马上总结改正。
---
## switch函数的原型
``` C++
switch (表达式) 
{
    case 常量1:
        // 当表达式等于常量1时执行的代码
        break; // 退出 switch 语句
    case 常量2:
        // 当表达式等于常量2时执行的代码
        break;
    // 可以有任意数量的 case
    default:
        // 如果没有 case 匹配，执行这里的代码
}
```
**注意**：`case`后面只能跟常量，意思是不能接变量（如`int a`或者`char c`），可以接常量`1`(数字常量)`'C'`（符号常量）`"This is a string"`(字符串常量)。

## switch函数的用法
笔者代码经历过少，不过认为switch主要做多重简单的判断。比如一个C++作业要求分别统计一个字符串中C、Q、U的出现次数，那么我们可以如下面这样操作：
```
    int countC = 0, countQ = 0, countU = 0; // 保存C、Q、U各自出现的次数：

while(i++<insert_string.size)
{
            switch (insert_string[i])
         { 
            case 'C': // 如果是大写字母 'C'
                countC++;
                break;
            case 'Q': // 如果是大写字母 'Q'
                countQ++;
                break;
            case 'U': // 如果是大写字母 'U'
                countU++;
                break;
        }
    }
}
  
```
至此，countC、countQ、countU中即分别是`insert_string`这个字符串（或者string类）中C、Q、U出现的次数了。

## 要注意的地方
switch一定要写`break`，其执行顺序是从上到下，某一个case条件一旦满足，就逐行执行（包括执行其下case的内容），直到switch语句结束。
比如如果不`break`，如果一次循环中，`insert_string[i] = ‘q’`，那么会执行countQ++，也会执行countU++。（逐行执行直到switch本次循环结束）
