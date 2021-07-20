```C++
// C++
class Solution {
public:
    int minDays(vector<int>& bloomDay, int m, int k) {
        // 二分
        int left = 0;
        int max = 0;
      
        // 上界为bloomDay数组中的最大值
        for (int i = 0; i < bloomDay.size(); i++){
            if (bloomDay[i] > max) max = bloomDay[i];
            else max = max;
        }
        // 加一，多一个无解
        max = max + 1; 
        int right = max;
      
        // 或者直接取1 <= bloomDay[i] <= 10^9的上届，复杂度相差很小
        // int max = 1000000001;
        // int right = 1000000001;

        while (left < right) {
            int mid = (left + right) / 2;
            if (isValid(bloomDay, m, k, mid)) right = mid;
            else left = mid + 1;
        }

        if (right == max) right = -1;
        return right;
    }

private:
    // 判定：第T天的开花情况，能否制作m束花，每束花都是相邻的k朵
    bool isValid(vector<int>& bloomDay, int m, int k, int T){
        // 统计制作花束的数量和连续的花朵数量
        int bouquet = 0;
        int sequent = 0;
        //
        for (int i = 0; i < bloomDay.size(); i++){
            if (bloomDay[i] <= T){ // 如果bloomDay小于T，说明花已经开了
                sequent++;
                // 当连续的花朵有k朵时，能制作的花束+1，同时将连续的花朵数量重置为0
                if (sequent == k){
                    bouquet++;
                    sequent = 0;
                }
            } else { // 当bloomDay大于T，花没有开，连续花朵数量为0
                sequent = 0;
            }
        }
        return bouquet >= m;
    }

};
```
