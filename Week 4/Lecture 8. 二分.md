## Lecture 8. 二分

### 二分查找

**二分查找的前提**  
- 目标函数具有单调性（单调递增或者递减）
- 存在上下界
- 能够通过索引访问（index accessible）

**代码模板**  

![image](https://user-images.githubusercontent.com/86143164/126110816-b461ded3-64fb-403f-81b3-de26b24c3700.png)

![image](https://user-images.githubusercontent.com/86143164/126110924-cd23dc60-2cbd-49bc-905f-4033779e869e.png)

**lower_bound与upper_bound**  
- 在单调递增数组里，如`[10,14,19,25,27,31,33,35,42,44]`，查找第一个`>=31`的数（返回其下标），不存在则返回`array.length`  
- 在单调递增数组里，如`[10,14,19,25,27,31,33,35,42,44]`，查找第一个`>26`的数（返回其下标），不存在则返回`array.length`

lower_bound与upper_bound的问题是：
- 给定的`target`不一定在数组中存在
- `array[mid]`即使不等于`target`，也节能就是最后的答案，不能随便排除在外

![image](https://user-images.githubusercontent.com/86143164/126111729-8d0bb0d6-9737-4e79-91d1-54f00c9d90d4.png)

**解决方案**  
三种二分法中的一种：
- 1.1 + 1.2: 最严谨的划分，一侧包含，一侧不包含，终止于`left == right`

![image](https://user-images.githubusercontent.com/86143164/126111971-51da33d4-06b0-4844-b8de-b7ee625d4f4a.png)

![image](https://user-images.githubusercontent.com/86143164/126112040-3686b6b5-5585-4958-983b-be50bfb632c4.png)

- 2: 双侧都不包含，用ans维护答案，终止于`left > right`

![image](https://user-images.githubusercontent.com/86143164/126112087-839b0b6c-6ce1-40ab-b4a9-68b22ae87dde.png)

- 3: 双侧都包含，终止于`left + 1 == right`，最后再检查答案

![image](https://user-images.githubusercontent.com/86143164/126112122-095e88e6-603e-494d-bba8-56a20dbf2737.png)

-------
### 三分查找

![image](https://user-images.githubusercontent.com/86143164/126112179-a3f3ce37-4182-47db-94cf-7f51d6fedceb.png)

三分法用于求单峰函数的极大值（或单谷函数的极小值）  
三分法也可用于求函数的局部极大/极小值  
要求：函数是分段严格单调递增/递减的（不能出现一段平的情况）  

以求单峰函数f的极大值为例，可在定义域`[l,r]`上取任意两点`lmid,rmid`
- 若`f(lmid) <= f(rmid)`，则函数必然在`lmid`处单调递增，极值在`[lmid,r]`上
- 若`f(lmid) > f(rmid)`，则函数必然在`rmid`处单调递减，极值在`[l,rmid]`上

![image](https://user-images.githubusercontent.com/86143164/126115308-fe7785de-623a-4dfd-9a6b-6eb73df1467f.png)

`lmid,rmid`可取三等分点，也可取`lmid`为二等分点，`rmid`为`lmid`稍加一点偏移量
**思考**：取黄金分割点最快？

-------
### 二分答案
对于一个最优化问题（求最大值/最小值问题）  
求解：求一个最优解（最大值/最小值）
判定：给一个解，判断它是否合法（是否能够实现）

“判定”通常比“求解”要简单很多，如果我们有了一个判定算法，那把解空间枚举+判定一遍，就能够得到解  
当解空间具有单调性时，就可以用二分代替枚举，利用**二分+判定**的方法快速求出最优解，这种方法称为二分答案法  
例如，求解




