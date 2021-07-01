## 递归、分治

### 递归(Recursion)

如何理解递归？
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
递推与递归在英语中都称为recursion，实际两者的区别是什么？
- 递推是从初始值开始反复进行某一相同的运算得到结果——从已知的`1! = 1`到未知的`6! = ?`
- 递归是从所需要的结果出发不断向上回溯，直到到达初始值再递推得到结果——从未知的`6! = ?`到已知的`1! = 1`
- 递归是























