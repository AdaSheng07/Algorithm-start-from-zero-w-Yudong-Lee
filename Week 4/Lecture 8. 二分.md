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
在单调递增数组里，如`[10,14,19,25,27,31,33,35,42,44]`，查找第一个`>=31`的数（返回其下标），不存在则返回`array.length`  
在单调递增数组里，如`[10,14,19,25,27,31,33,35,42,44]`，查找第一个`>26`的数（返回其下标），不存在则返回`array.length`

lower_bound与upper_bound的问题是：
