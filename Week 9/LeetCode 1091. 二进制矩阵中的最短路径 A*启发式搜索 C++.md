```C++
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {

        n = grid.size();
        // 特判：如果起点(0, 0)或终点(n - 1, n - 1)单元格的值是1，不存在畅通路径，返回-1
        if (grid[0][0] == 1 || grid[n - 1][n - 1] == 1) return -1;
        // 否则如果n = 1，返回1；如果n = 2，返回2
        else if (n <= 2) return n;

        // 设置单元格路径的移动方向数组，共八个方向
        vector<vector<int>> dirs;
        dirs = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};

        // 初始化起点为(0, 0)，终点为(n-1, n-1)
        // 换算后将cnt中的key存为0～(n * n) - 1，value存当前状态到达目标状态途径的单元格总数
        int x = 0, y = 0;
        int start = 0;
        cnt[start] = 1;
        int target = n * n - 1;
        // 优先队列BFS
        q.push(make_pair(n - 1, start));
        while (!q.empty()) {
            int now = q.top().second;
            // 由0～(n * n) - 1标号的索引now反推在grid中的单元格位置(x, y)
            x = now / n;
            y = now % n;
            q.pop();
            // 判断从(x, y)位置开始可移动到的相邻单元格位置
            for (auto dir : dirs) {
                int dx = x + dir[0];
                int dy = y + dir[1];
                int next = dx * n + dy;
                // cout << "("<< dx << ", " << dy << ")"<< endl;
                // 如果移动到了终点(n-1, n-1)，返回当前状态对应途径单元格数量+1
                if (dx == n - 1 && dy == n - 1) {
                    return cnt[now] + 1;
                }
                /* 如果(dx, dy)没有走过或者cnt[next]可被更新为更小值，
                   并且dx和dy都没有越界，grid[dx][dy]位置为0可以通过，
                   将目前通过单元格数+对未来进行估价，推入优先队列*/
                if ((cnt.find(next) == cnt.end() || cnt[next] > cnt[now] + 1)
                    && dx >= 0 && dx < n && dy >= 0 && dy < n 
                    && grid[dx][dy] == 0) {
                        // A*启发式搜索，估价模块
                        /* 假设所有单元格的值都是0，估价函数计算当下单元格到终点所需要的最短路径，此路径一定优于（<=）实际路径*/
                        int eval = max(abs(n - 1 - dx), abs(n - 1 - dy));
                        q.push(make_pair((- cnt[now] - eval), next));
                        cnt[next] = cnt[now] + 1;
                        // cout << "next = " << dx * n + dy << endl;
                        // cout << cnt[next] << endl;
                }
                if (cnt.find(target) != cnt.end()) return cnt[target];
            }
        }
        return -1;
    }

    int n; // 矩阵维度
    unordered_map<int, int> cnt; // 存入对应状态到达目标状态途径的单元格总数
    priority_queue<pair<int, int>> q; // 优先队列
};
```
