```C++
// C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        /* 寻找两个符合条件的目标值，是i, j的两层循环问题
        通过固定i，来寻找一个j使得nums[i] + nums[j] = target
        也就是在nums中寻找有没有元素值等于target - nums[i]
        利用一个映射value_to_index，返回符合条件的元素的数组下标 */ 
        unordered_map<int, int> value_to_index; 
        // 对i遍历
        for (int i = 0; i <= nums.size(); i++){
            // C++中map.find如果未找到结果，则返回尾指针，不等于尾指针则说明有结果
            if (value_to_index.find(target - nums[i]) != value_to_index.end()) {
                return {i, value_to_index[target - nums[i]]}; 
                // 此处value_to_index[target - nums[i]是在nums[0,...,i-1]中寻找
            }
            // 边循环i，边插入，维护对nums[0,...,i-1]的映射
            // 防止对nums[i]的自身映射
            value_to_index[nums[i]] = i; 
        } 
    return {}; // 如果没有符合条件的结果，返回空
    }
};

```
