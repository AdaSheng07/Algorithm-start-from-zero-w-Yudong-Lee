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

[子集](https://leetcode-cn.com/problems/subsets/)  
- 子集问题是一个指数型的问题，子集个数一定是`2^n`：每个元素都有选/不选两种可能，一共`n`个元素，即一共有`2^n`种方案
- 如果用暴力枚举法：`n`层循环，每层选/不选循环
- 用递归来描述数组元素选/不选的可能
  - 答案数组为全函数体共享的全局变量，构成一个数组`set`，`set`构成答案数组中的元素，也是全函数体共享的全局变量，随着递归不断被修改更新
  - 如果当前位置`index`不选，考虑下一个数选/不选，`index + 1`
  - 如果当前位置`index`选，将`nums[index]`放入数组`set`，再考虑下一个数选/不选，`index + 1`，递归结束时还原全局变量`set`，删除`set`中最后一个元素
  - 终止条件：递归从`index = 0`开始枚举选/不选，当`index = nums.length`，递归终止，同时将`set`结果拷贝进答案数组

[代码实现](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%2078.%20%E5%AD%90%E9%9B%86.md)  
*可在每次递归开始前打印`index`和`set`观察回溯

![image](https://user-images.githubusercontent.com/86143164/124070162-f6192480-da6f-11eb-814f-55b89218dcdc.png)

时间复杂度：最后一层结果为`2^n`个，所有层共有`2^n + 2^(n-1) + ... + 2 + 1 = 2^(n+1) - 1 <= 2^(n+1) = (2^n)·2`，即`O(2^n)`


组合

全排列



























