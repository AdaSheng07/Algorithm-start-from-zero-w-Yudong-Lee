```C++
class Solution {
public:
    int climbStairs(int n) {
        vector<int> f (n + 1, 0);
        for (int i = 0; i <= n; i++) {
            if (i == 0) f[i] = 0;
            if (i == 1) f[i] = 1;
            if (i == 2) f[i] = 2;
            if (i > 2) {
                f[i] = f[i - 1] + f[i - 2];
            }
        }
        return f[n];
    }
};
```
