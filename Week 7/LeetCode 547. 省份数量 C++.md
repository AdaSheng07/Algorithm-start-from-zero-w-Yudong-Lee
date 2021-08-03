```C++
class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        // 初始化并查集数组father
        for (int i = 0; i < isConnected.size(); i++) {
            father.push_back(i);
        }
        // 遍历isConnected考虑所有点的关系
        for (int i = 0; i < isConnected.size(); i++)
            for (int j = i + 1; j < isConnected.size(); j++)
                // 如果有1，合并
                if (isConnected[i][j] == 1) {
                    unionSet(i, j);
                }
        int ans = 0;
        // 根的数量 = 省份数量
        for (int i = 0; i < isConnected.size(); i++){
            if (find(i) == i) ans++;
        }
        return ans;
    }

private:

    void unionSet(int i, int j) {
        int x = find(i);
        int y = find(j);
        if (x != y) father[x] = y;
    }

    int find(int x) {
        if (x == father[x]) return x;
        return father[x] = find(father[x]);
    }

    vector<int> father;

};
```
