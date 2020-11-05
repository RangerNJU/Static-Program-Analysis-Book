# 指针分析二

1. Pointer Analysis: Rules
2. How to Implement Pointer Analysis
3. Pointer Analysis: Algorithms
4. Pointer Analysis with Method Calls

<img src="04-03-pointer2-analysis-spa.assets/image-20201105195029800.png" style="zoom:50%;" />

首先介绍常用数学符号，不会的同学可以复习一下离散数学。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105195154527.png" style="zoom:50%;" />

分别定义变量，域，对象（用下标标识是在第几行创建的对象），实例域和指针（是变量和实例对象的并），和指向关系。`X`表示笛卡尔积。

# Pointer Analysis: Rules

<u>*前排提示：与《数理逻辑》/《形式化语义》梦幻联动。没学过的同学也不要着急。*</u>

<img src="04-03-pointer2-analysis-spa.assets/image-20201105195524932.png" style="zoom:50%;" />

主要解释Rule一列中的内容。**横线上的内容是前提(Premises)，横线下的内容是结论(Conclusion)。**

用简单易懂的语言描述，看到new语句，我们就将新建的对象加入`pt(x)`。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105195943007.png" style="zoom:50%;" />

对于Assign语句，我们将x指向y指向的对象。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105195843958.png" style="zoom:50%;" />

对于Store和Load亦然。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105200112512.png" style="zoom:50%;" />

<img src="04-03-pointer2-analysis-spa.assets/image-20201105200123601.png" style="zoom:50%;" />

最后用一图总结。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105200412145.png" style="zoom:50%;" />

# How to Implement Pointer Analysis

*<u>别处的资料都没有全家桶，只介绍某些特殊情况下的分析算法。在这里你能喜提一个完整的指针分析算法全家桶。</u>*

本质上来说，指针分析是在指针间**传递**指向关系。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105200815104.png" style="zoom:50%;" />

>   ​	Key to implementation: when 𝑝𝑡(𝑥)is **changed**, **propagate** the **changed par**t to the **related pointers** of 𝑥

<img src="04-03-pointer2-analysis-spa.assets/image-20201105201018655.png" style="zoom:50%;" />

## 必要数据结构——指针流图

>   Pointer Flow Graph (PFG) of a program is a directed graph  
>   that expresses how objects flow among the pointers in the program.

图的两大要素是Node和Edge。我们定义Node是所有Pointers，一条x到y的Edge则标识x可能流向y（may flow to and also **be pointed to by**) 。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105201421501.png" style="zoom:50%;" />

一个例子，假设c和d一开始都指向`oi`。

<img src="04-03-pointer2-analysis-spa.assets/image-20201105201746860.png" style="zoom:50%;" />

因此，所有b所指向的对象更新时，都要传递到e中。这是一个求传递闭包(transitive closure)的过程。假如我们考虑j位置的一条新语句`b = new T();`：

<img src="04-03-pointer2-analysis-spa.assets/image-20201105201939088.png" style="zoom:50%;" />

**未完待续……**

<img src="04-03-pointer2-analysis-spa.assets/image-20201105202101633.png" style="zoom:50%;" />



# Pointer Analysis: Algorithms

# Pointer Analysis with Method Calls