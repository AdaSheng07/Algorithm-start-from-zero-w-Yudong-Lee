## 哈希表、集合、映射

### 哈希表

- 散列表
- 通过“关键码”（key）直接进行访问的数据结构

#### 组成

哈希表由两部分组成：
- **一个数据结构**：通常为链表、数组，但链表很难用索引进行访问，而数组只支持小整数作为下标
- **Hash函数**：输入“关键码”（key），返回数据结构的索引，可以将任意key（复杂信息）映射成一个小型信息/小整数，etc.

对外封装表现：`hash_table[key] = value`  
实际是在数据结构的`hash(key)`位置处存储了`value: data_structure[hash(key)] = value`，`hash(key)`是索引值

当`key`为整数时，可定义`hash(key) = value`，这时哈希表其实是一个数组，`key`自己就是下标。但在一般情况下，关键码`key`是一个比较复杂的信息，比如：很大的数、字符串等，这时候`key`不能直接作为数据结构的下标，Hash函数的必要性和功能就体现出来了，可以用Hash函数把复杂信息映射到一个较小的值域内，作为索引。

#### 哈希碰撞(Collisions)

- 两个不同的key被计算出同样的Hash结果
- 不可避免：复杂信息映射到更小的值域
- 减少几率：让数据尽可能均匀分布

常见解决方案：**开散列**（数组+链表的结构，“挂链”）
- 依然有`hash(key) = value`计算数组的下标
- 数组的每一个位置存储一个**链表**的表头指针，数组实际上为一个表头数组
- 每个链表保存具有同样Hash值的数据

开散列的完整结构图
![image](https://user-images.githubusercontent.com/86143164/123962371-f966ce80-d9e3-11eb-8722-08df0d0b01fa.png)

如果需要查询John Smith对应的结果，先对John Smith这个`key`进行hash函数运算，`hash(John Smith) = 152`，对位于`152`位置的`ListNode`进行遍历，，找到`"John Smith"`后返回`value = "521-1234"`。

开散列的时间复杂度
- 当数据分布比较均衡时：insert, lookup, delete均为O(1)
- 当数据全部被hash函数映射为相同的hash值时：最坏，insert, lookup, delete均为O(n)

-------

### 无序集合、映射的实现与应用

#### 集合（set）

- 存储不重复的元素
- `multiset`可存储重复元素
- 有序集合，遍历时按元素大小排列，一般用平衡二叉搜索树实现，时间复杂度`O(logN)`
- 无序集合，一般用hash实现，时间复杂度`O(1)`

#### 映射（map）

- 存储关键码（key）不重复的键值对（key-value-pair）
- 有序：遍历时按key大小排列，一般用平衡二叉搜索树实现，时间复杂度`O(logN)`
- 无序：一般用hash实现，时间复杂度`O(1)`

*语言内置的类型（int, string）可以直接放进set/map中使用

-------

#### 阅读C++, Java, Python相关文档

**C++**  

[unordered_set](https://www.cplusplus.com/reference/unordered_set/unordered_set/)
- Keys are immutable. Elements in an `unordered_set` cannot be modified, but can be inserted and removed. 
- Elements are not sorted in any particular order, but organized into buckets, allowing fast retrieval ofindividual elements based on their value. O(1)
- It is faster to access than `set` containers, but less efficient for **range iteration through a subset of elements**. 
- Properties:
  - Associative: referenced by `key`, not absolute position
  - Unordered
  - Set: The value of an element is also the key used to identify it.
  - Unique
  - Allocator-aware
- Member functions

| Command | Description |
| --- | --- |
| [insert](https://www.cplusplus.com/reference/unordered_set/unordered_set/insert/) | Insert elements |
| [find](https://www.cplusplus.com/reference/unordered_set/unordered_set/find/) | Get iterator to element |
| [erase](https://www.cplusplus.com/reference/unordered_set/unordered_set/erase/) | Erase elements |
| [clear](https://www.cplusplus.com/reference/unordered_set/unordered_set/clear/) | Clear content |
| [count](https://www.cplusplus.com/reference/unordered_set/unordered_set/count/) | Count elements with a specific key |

<br/>

[unordered_map](https://www.cplusplus.com/reference/unordered_map/unordered_map/)

- Assocative containers, store elements formed by the combination of a key value and a mapped value.
- Elements are not sorted in any particular order, but organized into buckets, allowing for fast retrieval of individual elements based on their keys. O(1)
- It is faster to access than `map` containers, but less efficient for **range iteration through a subset of elements**. 
- Types of key and mapped calue may differ. 
- Properties:
  - Associative: referenced by `key`, not absolute position
  - Unordered
  - Map: 
    - Each element associates a key to a mapped value.
    - Keys are meant to identify the elements whose main content is the mapped value.
  - Unique
  - Allocator-aware
- Definition
```C++
typedef pair<const Key, T> value_type;
```
- Iterators
```C++
unordered_map<Key,T>::iterator it;
(*it).first;             // the key value (of type Key)
(*it).second;            // the mapped value (of type T)
(*it);                   // the "element value" (of type pair<const Key,T>) 

it->first;               // same as (*it).first   (the key value)
it->second;              // same as (*it).second  (the mapped value) 
```
- Member functions

| Command | Description |
| --- | --- |
| [insert](https://www.cplusplus.com/reference/unordered_map/unordered_map/insert/) | Insert elements |
| [find](https://www.cplusplus.com/reference/unordered_map/unordered_map/find/) | Get iterator to element |
| [erase](https://www.cplusplus.com/reference/unordered_map/unordered_map/erase/) | Erase elements |
| [clear](https://www.cplusplus.com/reference/unordered_map/unordered_map/clear/) | Clear content |
| [count](https://www.cplusplus.com/reference/unordered_map/unordered_map/count/) | Count elements with a specific key |

**Java**  

[Set](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/Set.html)

[Set Examples](https://www.runoob.com/java/java-hashset.html)

[Map](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/util/Map.html)

[Map Examples](https://www.runoob.com/java/java-hashmap.html)

**Python**

[Set](https://www.runoob.com/python3/python3-set.html)

[Dict](https://www.runoob.com/python3/python3-dictionary.html)

-------
#### 例题

[LeetCode 1. 两数之和](https://leetcode-cn.com/problems/two-sum/description/)  

- 给定目标值`target`，求解求和的元素组合，暴力法为典型的两层for-loop循环返回数组索引值
- 主体思路：有一个`nums[i]`，寻找一个`j`使得`nums[i] = nums[j] = target`，即在`nums`中寻找`target - nums[i]`
- 细节：
 - 只能在除了`nums[i]`本身的其余元素中寻找，同一个元素不可重复出现
 - 题目对答案的顺序没有要求，可以设置`j < i`，有：
   ```
   for i = 1~,-1
     search if (target - nums[i]) in nums[0, 1,..., i-1]
   ```
 - 一边对`i`遍历，一边在map中插入`nums[i] = i`，维护对`nums[i]`的映射；同时，在`if`后进行插入操作避免了`nums[i]`的重复使用

[实现代码](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%201.%20%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.md) 

-------

[LeetCode 874. 模拟行走机器人](https://leetcode-cn.com/problems/walking-robot-simulation/)

- 主体思路：暴力解法，重点是解决障碍物问题以及左转右转90度问题
- 细节：
  - 判断障碍的两种方法：
    - 方案1: 将整数数组转变为string
    - 方案2: 将(x, y)看作进制数的第1和第0位，防止为负先平移坐标系再换算，转变为大整数long long
  - 左转右转问题可利用方向数组指导(x, y)的移动方向：  
    向北移动1时，x不变，y加一  
    向东移动1时，x加一，y不变  
    向南移动1时，x不变，y减一  
    向西移动1时，x减一，y不变  

[实现代码](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%20874.%20%E6%A8%A1%E6%8B%9F%E8%A1%8C%E8%B5%B0%E6%9C%BA%E5%99%A8%E4%BA%BA.md)

-------

[LeetCode 49. 字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

[实现代码](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%2049.%20%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D%E5%88%86%E7%BB%84%20%E4%BB%A3%E7%A0%81.md)

-------

[LeetCode 30. 串联所有单词的子串](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/)

- 如果用暴力法，假设`words`中有`k`个单词，考虑`words`中所有的排列顺序，时间复杂度为`O(k!)`爆炸
- 主体思路： 
  - 寻找`s`的子串：哪些是`words`的串联？
  - 寻找子串，最直接的方法是for-loop循环枚举，枚举完毕后，问题变为：给定一个string，判断它是否是`words`的串联，即string内部是否包含与`words`相同的单词
  - 也就是，找到一些单词，排列顺序无所谓，只要包含与`words`相同的内容
  - 参考49. 字母异位词分组的理念

[实现代码]

-------

#### 作业：实现一个LRU

[LeetCode 146. LRU缓存机制](https://leetcode-cn.com/problems/lru-cache/)

![image](https://user-images.githubusercontent.com/86143164/123986844-41dcb700-d9f9-11eb-9e4e-c81a926029fd.png)

- 为什么用链表？链表是在一组数的中间快速删除/插入元素的数据结构
- 利用哈希表+双向链表，解决链表不能快速查询的缺点：双向链表用于按时间顺序保存数据，哈希表用于把key映射到链表节点
- `O(1)`访问：直接检查哈希表
- `O(1)`更新：通过哈希表定位到链表节点，如果存在，删除此节点并在链表表头重新插入
- `O(1)`删除：注意边界问题，如果超出容量上限，总是淘汰链表的尾节点，同时在hashmap中删除对应的key-value pair

[实现代码](https://github.com/AdaSheng07/Algorithm-start-from-zero-w-YudongLee/blob/main/Week%202/LeetCode%20146.%20LRU%E7%BC%93%E5%AD%98%E6%9C%BA%E5%88%B6%20%E4%BB%A3%E7%A0%81.md)

