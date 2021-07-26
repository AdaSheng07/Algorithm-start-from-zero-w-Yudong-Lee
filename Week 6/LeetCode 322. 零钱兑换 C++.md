```C++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int INF = 1000000000;
        vector<int> opt (amount + 1, int());
        opt[0] = 0;
        for (int i = 1; i <= amount; i++) {
            opt[i] = INF;
            for (int j = 0; j < coins.size(); j++) {
                if (coins[j] <= i) {
                    opt[i] = min(opt[i], opt[i - coins[j]] + 1);
                }
            }
        }
        if (opt[amount] >= INF) opt[amount] = -1;
        return opt[amount];
    }
};
```
