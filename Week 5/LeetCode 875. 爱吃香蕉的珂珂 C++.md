```C++
// C++
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
      
        // 二分：
        int left = 1;
        int right = pow(10, 9);

        while (left < right) {
            int mid = left + (right - left) / 2;
            if (isValid(piles, h, mid)) right = mid;
            else left = mid + 1;
        }
        return right;
    }

    // 判定：吃香蕉的速度为k时的情况，能否在h小时内吃完piles内的所有香蕉
    bool isValid(vector<int>& piles, int h, int k) {
        int countHour = 0;
        for (int p : piles){
            countHour += (p - 1) / k + 1;
        } 
        return countHour <= h;
    }

};

```
