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

递归实现的暴力搜索：

![image](https://user-images.githubusercontent.com/86143164/124345946-9c9b2c00-dc0e-11eb-9cac-868f2a51eadc.png)


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
<br/>
    [子集递归模板](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/%E5%AD%90%E9%9B%86%E9%80%92%E5%BD%92%E6%A8%A1%E6%9D%BF.md)

-------

[组合](https://leetcode-cn.com/problems/combinations/)
- 组合是子集的一个特例，k个数的组合 = k个元素的子集  

**方案1:**
- 组合的实现可以在子集的实现形式基础上，在`1...n`中进行递归枚举，`num : [1, n]`，参数`num`取值改为在`[1, n]`间自增，当值为`n+1`时达到本次递归的一个终止条件
- 递归的第二个终止条件是当`set`中的元素数为k
- 所以整合递归的终止条件为：`num == n + 1`和`set.size() == k`，两条件均满足时，将当前的`set`拷贝进答案数组`ans`；只满足`num == n + 1`时，不拷贝`set`，直接进入下一次递归。以此方法实现时间复杂度仍然是`O(2^n)`，速度较慢

    [方案1 代码实现](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%2077.%20%E7%BB%84%E5%90%88%20%E6%96%B9%E6%A1%881.md)

**方案2:**  
- 增加一个提前判断排除不合法情况，以`n = 4, k = 2`为例：
  - 如果在递归枚举未终止时，`set`中的元素数量已经超过`k = 2`个，可退出此次递归枚举；
  - 或者，即使把剩下的所有元素全选`set`中的元素数量也不足`k = 2`个，也可以退出此次递归枚举
```Java
if (set.size() > k || set.size() + n - num + 1 < k) return;
```
- 时间复杂度：

    ![image](https://user-images.githubusercontent.com/86143164/124091189-25d42680-da88-11eb-8347-757a58970c7c.png)

  - 每种方案只算一次，不会有多余情况，只要一个分支在经过判断后能向下走，一定会至少产生一个答案，不合法的结果会在判断的时候立刻被删除。
  - 根据二项式定理，方案2时间复杂度一定小于方案1。

    ![image](https://user-images.githubusercontent.com/86143164/124092403-641e1580-da89-11eb-8b04-93e479affec8.png)

- 可以将方案2看作一个剪枝问题（pruning），仍然以`n = 4, k = 2`为例：

![image](https://user-images.githubusercontent.com/86143164/124148202-03f79580-dac2-11eb-9471-736ad4f2031a.png)


[组合递归模板](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/%E7%BB%84%E5%90%88%E9%80%92%E5%BD%92%E6%A8%A1%E6%9D%BF.md)

-------

[全排列](https://leetcode-cn.com/problems/permutations/)

- 不是考虑每个数选/不选，而是考虑下一个数放哪一个还没用过的数，所以需要维护一个“还未用过的数”的信息
- 递归的终止条件是每个位置都已经被填满，将已排列好的数组拷贝到答案数组中，再删除存放排列的数组的最后一个元素，将该元素的使用状态重置
- 时间复杂度：`O(n!)`

    [代码实现](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%2046.%20%E5%85%A8%E6%8E%92%E5%88%97.md)

全排列的回溯图解（以`nums = [1,2,3]`为例）：

![image](https://user-images.githubusercontent.com/86143164/124352203-a41ffc80-dc31-11eb-99b3-4be0c2971f1b.png)


[排列递归模板](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/%E6%8E%92%E5%88%97%E9%80%92%E5%BD%92%E6%A8%A1%E6%9D%BF.md)

-------

### 树

![image](https://user-images.githubusercontent.com/86143164/124353986-48a73c00-dc3c-11eb-85cf-4f989c300bb4.png)

-------

[翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)  

- 将每棵子树的内部都进行翻转，递归的子问题就是翻转一棵树的左和右
- 终止条件：达到边界叶子结点，无子树。当左右节点中有一个为`null`时，仍然可以翻转，只有当`root`已经无子树时，递归才达到边界  

[代码实现](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%20226.%20%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.md)

-------

[验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)  

- 二叉搜索树特征：节点的左子树只包含小于当前节点的数；节点的右子树只包含大于当前节点的数；所有左子树和右子树自身必须也是二叉搜索树
- 主体思路：如果遍历左右子树进行大小判断，效率太低，不妨改为：
  - 节点的左子树只包含小于当前节点的数 -> 左子树的最大节点比根小
  - 节点的右子树只包含大于当前节点的数 -> 右子树的最小节点比根大
- 对于一个子树的三个任务：
  - 求左子树的最大节点
  - 求右子树的最小节点
  - 验证是否是二叉搜索树

[代码实现](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%2098.%20%E9%AA%8C%E8%AF%81%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.md)

-------

### 分治

分治，指“分而治之”，就是把原问题划分成若干个同类子问题，分别解决后，再把结果合并起来。

关键点：
- 原问题和各子问题都是重复的（同类的）
- 除了向下递归问题，还要向上合并结果
- 一般用递归实现分治算法

![image](https://user-images.githubusercontent.com/86143164/124373983-e39a2780-dcc9-11eb-91ce-7ddb98d00b7d.png)

-------

[Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)


-------

[括号生成](https://leetcode-cn.com/problems/generate-parentheses/)






















