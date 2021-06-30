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

- 给定目标值`target`，求解求和




