```C++

class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        // 初始化dist数组，0～n，dist[0] = 0不用
        vector<int> dist (n + 1, 0);
        // 将所有位置初始值设为+∞
        for (int i = 1; i <= n; i++) dist[i] = int(1e9);
        // 起点位置k的值设为0
        dist[k] = 0;
        // Bellman-Ford algo
        // 共有n个结点，至多扫描更新n-1轮，round计数
        for (int round = 1; round < n; round++){
            // 设flag记录本次扫描是否有更新
            bool flag = false;
            for (auto edge : times) {
                int x = edge[0];
                int y = edge[1];
                int z = edge[2];
                // 判断：dist[y] > dist[x] + z？如果是说明dist[y]可更新
                if (dist[y] > dist[x] + z) {
                    dist[y] = dist[x] + z;
                    flag = true;
                } 
            }
            // 如果本轮扫描无更新，可提前结束，无需循环n-1轮
            if (!flag) break;
        }
        // result存取数组dist中的最大值
        int result = 0;
        for (int i = 0; i <= n; i++) {
            result = max(result, dist[i]);
        }
        // 如果result为+∞，说明有起点无法到达的结点，不能让所有结点都收到信号，返回-1
        if (result == 1e9) return -1;
        return result;
    }
};

```
