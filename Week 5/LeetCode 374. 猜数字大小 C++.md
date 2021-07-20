```C++
// C++
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is lower than the guess number
 *			      1 if num is higher than the guess number
 *               otherwise return 0
 * int guess(int num);
 */

class Solution {
public:
    int guessNumber(int n) {
        int left = 1;
        int right = n;
        while(left <= right) {
            // 防溢出写法
            int mid = left + (right - left) / 2;
            // 调用一次API取出猜测结果
            int flag = guess(mid);
            if (flag == 0) return mid;
            if (flag == -1) right = mid;
            else if (flag == 1) left = mid + 1;
        }
        return -1;
    }
};
```
