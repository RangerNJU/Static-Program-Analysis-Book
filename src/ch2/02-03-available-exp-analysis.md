# 数据流分析之可用表达式分析

## 定义

> An expression x op y is available at program point p if (1) all paths from the entry to p must pass through the evaluation of x op y, and (2) after the last evaluation of x op y, there is no redefinition of x or y.

## 理解定义：一个tricky的例子

1. 按照直觉来说，c处不是，但是按照定义来说是。但是实际上运行时只会走一条分支。

2. 回顾：
must->under-approximation->报出来的全都是真的。不允许误报，但允许漏报
may->不允许漏报，但允许误报
重新理解这个例子。

PS. 如何记住边界条件设置谁？设置是空还是满？对余下所有块的初始化是空还是满（一个巧妙的方法是判断may/must后，如果条件汇合时是交集，一般开始时大多数块初始化为满。）

一个经常迷惑的问题：先gen先kill？根据定义就解决所有问题2
