# W1 Key Points Summary & Homework

加一[Link to a header](#lc66-加一-Easy)

### Array 数组

#### 时间复杂度
lookup  O(1)  
insert  O(n)  
delete  O(n)  
append(push back)  O(1)  
prepend(push front)  O(n) 

#### 变长数组




-------
#### LC88 合并两个有序数组 Easy
https://leetcode-cn.com/problems/merge-sorted-array/description/
- `nums1`与`nums2`均为有序数组，且`nums1`空间已经开辟好，有足够的空间保存来自`num2`的元素
- 主体思路：`i, j`两个索引自增后比较数组元素大小，谁小放谁
- 细节问题：
  - 索引的边界处理
  - 防止合并后的新数组元素覆盖`num1`的原有数组元素：
    - 建立新数组，合并完成后拷贝进`num1`
    - 倒放合并数组元素，`i`与`j`自减，不需要新数组`nums3`
```C++
  // C++
  // 归并排序的基本操作
  int i = m - 1, j = n - 1, k;
  for (k = m + n - 1; k >= 0; k--){ // k从nums1的末尾开始放置
  // 利用j < 0 || i >= 0或者if (i < 0 || j < 0) break; 来对i, j索引的边界进行预先判断
      if (j < 0 || (i >= 0 && nums1[i] >= nums2[j])){
          nums1[k] = nums1[i];
          i--;
      }else{
          nums1[k] = nums2[j];
          j--;
      }
  }
  // 时间复杂度为O(n)
```
-------
#### LC26 删除有序数组中的重复项 Easy
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/
- 原地修改有序数组，不能开辟新的数组空间
- 主体思路：因为数组有序，则一个元素与前面的元素不相同时保留，相同时删除
- 细节：
  - 索引越界问题：当`i = 0`时，`nums[0]`是必然保留的，解决`i - 1`的越界
  - 编辑过的数组元素数量一定小于等于原数组长度，故不存在覆盖问题
```C++
  // C++
  int removeDuplicates(vector<int>& nums) {
      int i, n = 0;
      for (i = 0; i < nums.size(); i++){
          if (i == 0 || nums[i] != nums[i - 1]){
          nums[n] = nums[i];
          n++;
          }
      }
      return n;
  }
  // 时间复杂度为O(n)
	
```

#### LC283 移动零 Easy
https://leetcode-cn.com/problems/move-zeroes/
- 在原数组操作，将所有零移动到数组末尾，同时保证非零元素的相对顺序
- 主体思路：当数组中一个元素不等于零，就保留这个元素
- 细节：
  - 是否保留元素的判断条件
  - 在非零元素保留之后补零：
  ```C++
    // C++
    // 补零模块
    while (n < nums.size()) {
        nums[n] = 0;
        n++;
    }
    // 完整代码for-loop循环n次，时间复杂度为O(n)
  ```
<br/>

> LC26去重与LC283移动零这两题的实现思路是相同的：满足怎样的条件式即可对数组元素实行原地操作，同时考虑索引边界与原数组的被覆盖问题。

-------

#### LC66 加一 Easy
https://leetcode-cn.com/problems/plus-one/
- 主体思路：两种方法
  1. 在数组基础上直接判断每一位的数字是否等于9，是否需要进位  
  2. 将数组还原为x位数，加一后再逐位分离为单一数字，存入一个新数组  
  方法2在处理加一时的进位问题看上去非常简单，但是将数组还原为数字需要`for-loop`，后期还需要判断加一后数字的位数，将它们的每一位分离，并利用`for-loop`将每位位数存入新数组。对比来看方法1在数组上直接操作，更为简便。
- 细节：
  - 如果`digits`的最后一个元素非9，则对最后一个元素加一后返回`digits`
  - 如果`digits`的最后一个元素为9，则使最后一个元素为0，倒数第二个元素加一：
    - 对倒数第二个元素需要做判定，如果为9，则使其为0，再向前进一位；再进行判定...以此类推
```C++
// C++ 完整代码
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        // 从最后一位开始判断是否为9和加一
        for (int i = digits.size() - 1; i >= 0; i--) {
            if (digits[i] != 9) {
                digits[i] += 1;
                return digits;
            }
            // 如果该位为9，加一则变为0，前一位进一
            digits[i] = 0;
        }
        // 如果经过以上for-loop后仍然没有return
        // 说明digits的每一位都是9
        // 此时有溢出，需要建立一个首元素为1，其余皆为0新数组
        vector<int> temp (digits.size() + 1, 0);
        temp[0] = 1;
        return temp;
    }
};
// 最坏时间复杂度为O(n)
```


<br/>

### Linked List 链表
-------
#### LC21 合并两个有序链表 Easy 模板题
https://leetcode-cn.com/problems/merge-two-sorted-lists/



-------
#### LC206 反转链表 Easy
https://leetcode-cn.com/problems/reverse-linked-list/
- 输入一个头节点，返回一个头节点，返回的头节点指向为反转的原链表
- 主体思路：因为末节点指向`null`，`n`个节点的链表，需要更改`n`条边，将指向`next`节点改为指向`last`节点，而单链表只能向后访问，没有`last`节点，故需要开辟一个新变量用来记录`last`节点
- 细节：
	- 更改每条边需要访问链表，只要`head`节点不为`null`，则把`head`节点变为`next`节点：
  ```Java
  // Java
  // 访问链表的模版
  while (head != null) {
      head = head.next;
  }
  ```
	- `head.next`被更改（改`n`条边），`last`与`head`向后移动，需要用临时变量存储原本的`head.next`节点
	- `last`需要更新，当`head`向后移动一位，`last`也变成移动之前的`head`
```Java
// Java
// 完整代码
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode last = null;
        // 需要访问列表
        while (head != null) {
            // 更改每一条边，使得head的next指向head的last
            // 这导致head.next的值被更改，所以需要预先存储原来的head.next
            ListNode next_head = head.next;
            head.next = last;
            // last和head向后移动一位，last变为当前的head，head再更新
            last = head;
            head = next_head;
        }
        // 当head == null时，last为null之前的节点，故返回last
        return last;
    }
}
// 测试时可用空链表[]，看是否会崩溃
```
-------
#### LC25 k个一组反转链表 Hard
https://leetcode-cn.com/problems/reverse-nodes-in-k-group/
- 主体思路：
  - 模块化处理Hard问题，首先明确我们的任务可以分为分组和反转
  - 分组：`k`个节点一组，找到每个组的`head`与`end`，按分好的组逐一遍历
  - 反转：将每个组从`head`到`end`之间进行反转，可以参考LC206的反转链表模板
- 细节：
  - 分组问题的重点在于找到每个组的`end`，可以写一个`getEnd`的函数模板
    - 当`head`不为`null`时，`k`个节点分为一组，从`head`开始走`k - 1`步后返回的节点为`end`
    - 如果剩余节点不足`k`个则返回`null`
    - 当`k`为`0`时，返回当前`head`节点为`end`
    ```Java
    // Java
    // 向后走k-1步找到k个一组的组末尾节点
    private ListNode getEnd(ListNode head, k) {
        while (head != null){
            k--;
            if (k == 0) return head; // 或者break;
            head = head.next;
        }
    }
    return head;
    ```
  - 组内实现反转问题可以参考LC206的反转链表模板，但在此问题中的实现有流程区别。以`1→2→3→4→5，k = 2`的分组反转中间的`3→4`为例，可分为三步：
    - 每组的组内反转只需要更改`k - 1`条边，而不是`k`条边，因为组内的`end`节点后无`null`
    - 在组内反转之后，当前组`4→3`与前后被反转的组需要重新相连：
      - 前一组的新结尾`1`（旧`head`）→ 当前组的新开头`4`（旧`end`）
      - 当前组的新结尾`3`（旧`head`）→ 后一组的新开头`5`（旧`end`）

  - 为防止第一个节点的`last`为`null`，建立一个保护节点，再开始分组遍历；同时，建立保护节点也取消了第一个分组位于头部的特性，在返回最终结果时，不需要再寻找第一组的旧`end`，而可以直接返回保护节点的`next`，即第一组的新`head`（旧`end`）
  - 后一组的新`head`原本是`end.next`，但因为`end.next`在`reverseList`中被反转，所以需要提前把反转之前的`end.next`临时存储
  - 边界问题：
    - 访问节点的`next`之前，如果`getEnd`得到的是`null`，说明剩余节点不足`k`个，不需要反转，保持原有顺序
    - 当`while`遍历到最后`head == end`时，`end(head)`仍要指向上一个`last`

```Java
// Java 完整代码
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        // 建立保护节点
        ListNode protect = new ListNode(0, head);
        // 分组，找到每一组的head与end，再每组逐一遍历
        // 需要前一组的关系，last需要维护
        ListNode last = protect; // 防止last为空，利用保护节点
        while (head != null) {
            ListNode end = getEnd(head, k);

            if (end == null) break; 
            ListNode next_group_head = end.next; // 提前存储后一组的head
            // 在head和end之间进行组内反转
            reverseList(head, end);
            // 前一组的新结尾（旧head）→ 当前组的新开头（旧end）
            last.next = end;
            // 当前组的新结尾（旧head）→ 后一组的新开头（旧end）
            head.next = next_group_head;

            last = head; // 将上一组的结尾更新为当前组的新结尾
            head = next_group_head; // 将当前组的开头更新为下一组的新开头

        }
        return protect.next; // 保护节点的next是成组反转后的链表开头
    }

    // 向后走k-1步找到k个一组的组末尾节点
    private ListNode getEnd(ListNode head, int k) {
        while (head != null){
            k--;
            if (k == 0) return head; // 或者break;
            head = head.next;
        }
        return head;
    }

    // 在head和end之间进行组内反转后与前后组重新连接
    public void reverseList(ListNode head, ListNode end) {
        if (head == end) return; // 如果k = 1，返回原有链表
        // end后无null，组内需要更改k-1条边，遍历当前分组
        ListNode last = head;
        head = head.next;
        while (head != end) {
            ListNode next_head = head.next;
            // 改一条边
            head.next = last;
            // last和head向后移动一位，last变为当前的head，head再更新
            last = head;
            head = next_head;
        }
        end.next = last; // 遍历到最后head == end，需要end指向上一个last
    }
}
```
-------
#### LC141 环形链表 Easy
https://leetcode-cn.com/problems/linked-list-cycle/

#### LC142 环形链表 Medium
https://leetcode-cn.com/problems/linked-list-cycle-ii/

-------
### Stack Queue 栈 队列

#### Reading 不同语言中所带的栈、队列、双端队列、优先队列library与使用方法

C++: stack, queue, deque, priority queue

<br/>

Java: 
- Stack
- Queue, Deque可以用LinkedList实现
- PriorityQueue

<br/>

Python
- stack, queue, deque可以用list实现
- 优先队列可以用heapq库

-------
#### LC20 有效的括号 Medium
https://leetcode-cn.com/problems/valid-parentheses/
- 与最近相关性有关的题目适合用栈来处理

#### LC155 最小栈 Medium
https://leetcode-cn.com/problems/min-stack/


#### LC150 逆波兰表达式求值 Medium
https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/

-------
#### LC224 基本计算器 Hard
https://leetcode-cn.com/problems/basic-calculator/


-------
### 前缀和

#### 一维前缀和

设一维数组A与其对应的前缀和数组S，则有：

![image](https://user-images.githubusercontent.com/86143164/122957868-ee44ea80-d3b4-11eb-858a-4cd041519176.png)

如果计算数组A中从第`l`个数到第`r`个数的和，用暴力解法则需要对从`l`到`r`进行`for-loop`循环，每次的加法次数为`r-l+1`，最坏的时间复杂度为`o(n)`。而`o(1)`的计算子段和的方法为：

![image](https://user-images.githubusercontent.com/86143164/122960714-44fef400-d3b6-11eb-9492-cd4c80fd848b.png)

当数组A中元素皆为非负数时，前缀和数组S单调递增。

#### 二维前缀和

设二维数组`A`与其对应的前缀和数组`S`，利用容斥原理，可知求二维前缀和的推导式：

![image](https://user-images.githubusercontent.com/86143164/123026876-7a83fb80-d40f-11eb-8515-5fccdb176d30.png)

如果求二维数组的子矩阵和，即以`(p,q)`为左上角，`(i,j)`为右下角的A的子矩阵中数的和，有：

![image](https://user-images.githubusercontent.com/86143164/123027070-cc2c8600-d40f-11eb-963b-ca20149aaf9e.png)

预处理`O(n^2)`，询问`O(1)`的时间复杂度，暴力方法询问也是`O(n^2)`

前缀和算法不只局限于求和，也可以扩展到前缀最小值、最大值等问题。

-------
#### LC1248 统计「优美子数组」 Medium
https://leetcode-cn.com/problems/count-number-of-nice-subarrays/
- 如果某个连续子数组中恰好有`k`个奇数数字，这个子数组就是「优美子数组」，返回这个数组中「优美子数组」的数目
- 主体思路：连续数组转变为前缀和问题
  - 将数组元素变奇偶性，对2取模，剩下1和0
  - 子段里含有`k`个奇数数字就等价于子段里有`k`个1，即统计有多少连续子数组（子段）的和为`k`
  - 暴力枚举法：将两个循环变量分离，当`r`在`1-n`在外层遍历，固定外层后`l`在`1-r`内层遍历，如果满足前缀和`s[r] - s[l-1] == k`的条件，统计数目加一，此方法最坏为`O(n)`
  - 在暴力枚举法基础上的优化：固定外层循环变量后，考虑内层满足的条件  
    对于每个`r(1~n)`，有几个`l(1~r)`，可以满足`s[r] - s[l-1] = k`  
    对于每个`i(1~n)`，有几个`j(0~i-1)`，可以满足`s[i] - s[j] = k`  
    对于每个`i(1~n)`，有几个`j(0~i-1)`，可以满足`s[j] = s[i] - k`  
    对于每个`i(1~n)`，有几个`s[j], j(0~i-1)`等于`s[i] - k`  
    也就是统计数组`s`中，遍历`s[i]`后，等于`s[i] - k`的数的元素数量  
- 细节：
  - 将数组`nums`下标从`0~n-1`变为`1~n`，方便编程，再对2取模计算前缀和数组：
  ```Python3
  # Python 3
  # 将下标从0～n-1变为1～n
  nums = [0] + nums
  # 初始化前缀和数组s
  s = [0] * len(nums)
  # 对nums中的元素对2取模，奇偶性，变为0与1
  # 再求取前缀和数组s
  for i in range(1, len(nums)):
      s[i] = s[i - 1] + nums[i] % 2
  ```
  - 为了避免`for i for j`的最坏`O(n^2)`双层循环，先利用`count`数组计数，统计s[i]中各取值元素的数量：
  ```Python 3
  # Python 3
  # 对于数组s中，遍历s[i]后，等于s[i] - k的数的元素数量
  # 初始化一个计数数组count，先统计s[i]各元素数量
  count = [0] * len(s)
  for i in range(0, len(s)):
      count[s[i]] += 1
  ```
  - 再对`i`进行遍历，在`count`数组中寻找值等于`s[i] - k`的元素数量；在访问数组下标前，增加对于边界的判断：
  ```Python3
  # Python3
  # 在count数组中寻找值等于s[i] - k的元素数量
  ans = 0
  for i in range(0, len(nums)):
      if s[i] - k >= 0: # 注意下标越界问题
          ans += count[s[i] - k]
  ```
-------
#### LC304 二维区域和检索-矩阵不可变 Medium 模板题
https://leetcode-cn.com/problems/range-sum-query-2d-immutable/


-------
### 差分

设一维数组`A`，对应前缀和数组为`S`，`A`对应差分数组为`B`，其中`B[1] = A[1], B[i] = A[i] - A[i-1] (2<=i<=n)`

![image](https://user-images.githubusercontent.com/86143164/123039996-98f4f180-d425-11eb-8c55-0b49559618f4.png)

差分数组`B`的前缀和数组就是原数组`A`，前缀和数组`S`的差分数组也是原数组`A`。前缀和与差分是一对互逆运算，对一个数组先后进行前缀和运算和差分运算后仍为其本身。前缀和运算为计算前`i`个元素的和，只需要访问，而不需要修改。差分运算则是在原数组基础上进行修改值。

假设对一个数组的第2～4个元素加1后再对第3～4个元素减2:

![image](https://user-images.githubusercontent.com/86143164/123041194-93001000-d427-11eb-91b3-7868d803e556.png)

如果采用如图的暴力算法，先`for-loop`第2～4个元素加1，再`for-loop`第3～4个元素减2，最坏时间复杂度为`O(m·n)`。

如何在这种情况下利用差分？

观察当对`A`数组的第2～4个元素加1后其差分数组`B`的变化：

  ![image](https://user-images.githubusercontent.com/86143164/123042125-e9ba1980-d428-11eb-829b-3842e7c0f263.png)

再对`A'`数组第3～4个元素减2后其差分数组`B'`的变化:

  ![image](https://user-images.githubusercontent.com/86143164/123042367-4ddcdd80-d429-11eb-927c-1c48d46a637e.png)

可以总结出：  
把`A`的第`l`个数到第`r`个数加d，`A`的差分数组`B`的变化为：`B[l]`加d，`B[r+1]`减d。

  ![image](https://user-images.githubusercontent.com/86143164/123043117-6d283a80-d42a-11eb-85ec-689ce5044a8c.png)

每次操作只对两个元素，时间复杂度为`O(2m)=O(m)`。再对差分数组`B`求前缀和，就可以得到修改后的原数组`A''`。

常见应用：每次操作于一个区间的相同跨度的值变化，例如航班预订座位变化等。

-------

#### LC1109 航班预订统计 Medium 模板题
https://leetcode-cn.com/problems/corporate-flight-bookings/
- 主体思路：裸题，可直接带入差分运算和前缀和运算来求得变化后的原数组，思考每一个操作对结果的影响，影响的两个位置———从哪里开始到哪里结束，累加影响即为求前缀和。以示例1为例，利用上面的差分数组变化模板：
  ![image](https://user-images.githubusercontent.com/86143164/123044437-38b57e00-d42c-11eb-925a-17958e2e4b36.png)
- 细节：
  - 考虑到对`n+1`处“溢出”的操作，差分数组`diff`的长度应该是0～n+1
  - 差分模板：在差分数组`diff`的`bookings[0]`处加`bookings[2]`，在`bookings[1] + 1`处减`bookings[2]`
  ```C++
  // C++
  // 拆分每一组航班预订座位变化
  int first = booking[0];
  int last = booking[1]; 
  int seats = booking[2]; 
  // 差分模板实现：每一次操作对两个位置的影响
  // 在差分数组的first处加seats，在(last + 1)处减seats
  diff[first] += seats;
  diff[last + 1] -= seats;
  ```
  - 遍历`i`进行对`diff`差分数组进行前缀和计算之后得到的`prefix`数组为1～n，需要再次将`prefix`移位到0～n-1
  ```C++
  // C++
  // 初始化前缀和数组prefix
  vector<int> prefix(n + 1, 0); // 前缀和数组0～n

  // 遍历i对差分数组diff进行前缀和计算
  for (int i = 1; i <= n; i++){
      prefix[i] = prefix[i-1] + diff[i]; // 前缀和数组1～n
  }

  // 对前缀和数组prefix进行移位到0～n-1
  for (int i = 1; i <= n; i++) prefix[i-1] = prefix[i]; // i-1边界无问题
  prefix.pop_back(); // 全部移位后删除最后一个元素prefix[n]
  return prefix;
  ```

-------

#### LC53 最大子序和 Easy
https://leetcode-cn.com/problems/maximum-subarray/
- 找到整数数组`nums`中一个具有最大和的连续子数组（子数组最少包含一个元素）并返回其最大和
- 主体思路：在前缀和问题中，首先改变为前缀和相减的形式
  - 解法一：前缀和+前缀最小值
    - 求出前缀和数组`S`，枚举其右端点`i`固定，避免`O(n^2)`的双层循环，需要找到在`i`之前的一个`j`使得`S[i] - S[j]`最大，即让`S[j]`最小，再对`S[j]`维护一个`S`的前缀最小值——预处理前若干个`S`数组元素的前缀最小值并存储，再枚举`i`来做`S[i] - S[j]`运算
    - 
  



-------






















