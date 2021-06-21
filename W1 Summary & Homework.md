# W1 Summary & Homework

## Homework

### Array 数组
-------
#### LC88 合并两个有序数组 EASY
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
#### LC26 删除有序数组中的重复项 EASY
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

#### LC283 移动零 EASY
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
#### LC206 反转链表 EASY
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
```

































