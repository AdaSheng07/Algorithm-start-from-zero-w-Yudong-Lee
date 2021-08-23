在`C++`中，`multiset`是`<set>`库中一个非常有用的类型，它可以看成一个序列，插入一个数，删除一个数都能够在`O(logn)`的时间内完成，而且他能时刻保证序列中的数是有序的，而且序列中可以存在重复的数。
</br>
1. 在`C++`中`set/multiset`是有序的集合，它们是基于红黑树实现的。其中`set`会对元素去重，而`multiset`可以有重复元素;
2. 在`Java`中`TreeSet`是有序的集合，它也是基于红黑树实现的。`TreeSet`会对元素去重;
3. 在`Python`中`heapq`实现了堆的算法，它不会对元素去重。

参考：
</br>
[multiset用法总结](https://blog.csdn.net/sodacoco/article/details/84798621)
</br>
[C++ multiset的用法](https://www.acwing.com/file_system/file/content/whole/index/content/1744068/)

```C++

#include <set>

class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> ans;
        multiset<int> window;
        int left = 0;
        int i = 0;
        while (i <= k + left - 1 && i < nums.size()) {
            window.insert(nums[i]);
            if (i == k + left - 1) {
                ans.push_back(*window.rbegin());
                window.erase(window.find(nums[left]));
                left++;
            }
            i++;
        }
        return ans;
    }
};

```
