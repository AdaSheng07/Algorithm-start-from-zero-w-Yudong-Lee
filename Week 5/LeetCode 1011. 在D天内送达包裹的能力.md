```C++
// C++
class Solution {
public:
    int shipWithinDays(vector<int>& weights, int days) {
        // 二分上下界
        // left: weights中元素最大值
        // right: weights中所有元素之和
        int left = 0;
        int right = 0;
        for (int i = 0; i < weights.size(); i++) {
            left = max(left, weights[i]);
            right = right + weights[i];
        }
        // 二分
        while (left < right) {
            int mid = (left + right) / 2;
            if (isValid(weights, days, mid)) right = mid;
            else left = mid + 1;
        }
        return right;
    }

private:
    // 判定：最低载重为T时，能够在D天内将所有包裹送达
    bool isValid(vector<int>& weights, int days, int T) {
        int weight = 0;
        int day = 1; 
        for (int i = 0; i < weights.size(); i++) {
            // 如果最低载重可以承受
            if (weight + weights[i] <= T) {
                weight += weights[i];
            } else {
                // 如果最低载重不能承受，第二天另外运送
                weight = weights[i];
                day++;
            }
        }
        return day <= days; // 能否在D天以内将所有包裹送达？
    }
};
```
