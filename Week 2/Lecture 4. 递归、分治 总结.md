## 递归、分治

### 递归(Recursion)

#### 如何理解递归？
- 函数自身调用自身
- 通过函数体来进行的循环
- 以自相似的方法重复进行的过程

Example：计算n!  
n! = 1 * 2 * 3 ... * n
``` Python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)
```
此递归函数计算`factorial(6)`的实现路径：
```
factorial(6)
6 * factorial(5)
6 * (5 * factorial(4))
6 * (5 * (4 * factorial(3)))
6 * (5 * (4 * (3 * factorial(2))))
6 * (5 * (4 * (3 * 2 * (factorial(1)))))
6 * (5 * (4 * (3 * 2 * (1))))
6 * (5 * (4 * (3 * 2)))
6 * (5 * (4 * 6))
6 * (5 * 24)
6 * 120
720
```
递归函数计算`factorial(6)`也可以用for-loop递推实现：
```C++
int result = 1;
for (int i = 0; i <= 6; i ++) result = result * i;
return result; 
```
#### 递推与递归

在英语中都称为recursion，实际两者的区别是什么？
- 递推是从初始值开始反复进行某一相同的运算得到结果——从已知的`1! = 1`到未知的`6! = ?`
- 递归是从所需要的结果出发不断向上回溯，直到到达初始值再递推得到结果——从未知的`6! = ?`到已知的`1! = 1`
- 递归是从归纳法（Induction）衍生而来的

为什么倾向于用递归，而不是递推？

在计算`n!`的此例中，阶乘的计算推导路径是明确的，所以只需要for-loop一遍即可，但在有些情况下（比如树节点遍历），无法知道具体的路径。

![image](https://user-images.githubusercontent.com/86143164/124054817-61093200-da55-11eb-852b-a644bf9e53ac.png)

#### 递推的三个关键
- 定义需要递归的问题（重叠子问题）——数学归纳法思维
- 确定递归边界：不能无限递归，设定终止条件
- 保护和还原现场
  - 在递归过程中，局部变量和参数不需要恢复，属于每一个各自的函数体，在函数体终止时被自然释放
  - 所有的（静态）全局变量，`class`内的成员，所有函数体共享，在递归结束时回到上一个问题前需要被还原成前一个状态

#### 伪代码模板

![image](https://user-images.githubusercontent.com/86143164/124055573-b7c33b80-da56-11eb-9ecb-7f37afb68308.png)

![image](https://user-images.githubusercontent.com/86143164/124055598-c3aefd80-da56-11eb-9111-bd7b78c602b0.png)

#### 递归问题的三个基本实现形式

子集

组合

全排列



























