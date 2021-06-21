# W1 Summary & Homework

## Homework

### Array 数组
-------
#### LC88 合并两个有序数组 EASY
https://leetcode-cn.com/problems/merge-sorted-array/description/
- nums1与nums2均为有序数组，且nums1空间已经开辟好，有足够的空间保存来自num2的元素
- 主体思路：i, j两个索引自增后比较数组元素大小，谁小放谁
- 细节问题：
  - 索引的边界处理
  - 防止合并后的新数组元素覆盖num1的原有数组元素：
    - 建立新数组，合并完成后拷贝进num1
    - 倒放合并数组元素，i与j自减，不需要新数组nums3
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
```
-------
#### LC26 删除有序数组中的重复项 EASY
https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/
- 原地修改有序数组，不能开辟新的数组空间
- 主体思路：因为数组有序，则一个元素与前面的元素不相同时保留，相同时删除






























