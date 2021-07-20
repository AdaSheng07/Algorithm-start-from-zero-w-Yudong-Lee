```C++
// C++
class Solution {
public:
    int splitArray(vector<int>& nums, int m) {
        // lowerbound 每个数组元素单位单为一组，下界为数组中元素的最大值
        // upperbound 所有数组元素全部分为一组，上界为数组中所有元素的和
        int left = nums[0];
        int right;
        for (int i = 0; i < nums.size(); i++){
            left = max(nums[i], left);
            right += nums[i];
        }
        // 二分
        while (left < right) {
            int mid = (left + right) / 2;
            if (isValid(nums, m, mid)) right = mid;
            else left = mid + 1;
        }
        return left;
    }

    // 判定 把nums分成<=m组，每组的和<=T
private:
    bool isValid (vector<int>& nums, int m, int T) {
        int groupSum = 0;
        int groupCount = 1;
        for (int i = 0; i < nums.size(); i++){
            if (groupSum + nums[i] <= T){
                groupSum += nums[i];
            } else {
                groupCount++;
                groupSum = nums[i];
            }
        }
        return groupCount <= m;
    }

};
```
