# W1 Key Points Summary & Homework

### Array 数组
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
    // 补零模块
    while (n < nums.size()) {
        nums[n] = 0;
        n++;
    }
    // 完整代码for-loop循环n次，时间复杂度为O(n)
  ```
<br/>

> LC26去重与LC283移动零这两题的实现思路是相同的：满足怎样的条件式即可对数组元素实行原地操作，同时考虑索引边界与原数组的被覆盖问题。
<br/>

### Linked List 链表
-------
#### LC206 反转链表 Easy
https://leetcode-cn.com/problems/reverse-linked-list/
- 输入一个头节点，返回一个头节点，返回的头节点指向为反转的原链表
- 主体思路：因为末节点指向`null`，`n`个节点的链表，需要更改`n`条边，将指向`next`节点改为指向`last`节点，而单链表只能向后访问，没有`last`节点，故需要开辟一个新变量用来记录`last`节点
- 细节：
	- 更改每条边需要访问链表，只要`head`节点不为`null`，则把`head`节点变为`next`节点：
  ```Java
  // 访问链表的模版
  while (head != null) {
      head = head.next;
  }
  ```
	- `head.next`被更改（改`n`条边），`last`与`head`向后移动，需要用临时变量存储原本的`head.next`节点
	- `last`需要更新，当`head`向后移动一位，`last`也变成移动之前的`head`
```Java
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
// 完整代码
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


-------
### 前缀和

设一维数组A与其对应的前缀和数组S，则有：

![image](https://user-images.githubusercontent.com/86143164/122957868-ee44ea80-d3b4-11eb-858a-4cd041519176.png)

如果计算数组A中从第`l`个数到第`r`个数的和，用暴力解法则需要对从`l`到`r`进行`for-loop`循环，每次的加法次数为`r-l+1`，最坏的时间复杂度为`o(n)`。而`o(1)`的计算子段和的方法为：

![image](https://user-images.githubusercontent.com/86143164/122960714-44fef400-d3b6-11eb-9492-cd4c80fd848b.png)

当数组A中元素皆为非负数时，前缀和数组S单调递增。

-------
#### LC1248 统计「优美子数组」 Medium
https://leetcode-cn.com/problems/count-number-of-nice-subarrays/
- 如果某个连续子数组中恰好有`k`个奇数数字，这个子数组就是「优美子数组」，返回这个数组中「优美子数组」的数目
- 主体思路：
  - 将数组元素变奇偶性，对2取模，剩下1和0





































