```C++
class Solution {
public:
    int slidingPuzzle(vector<vector<int>>& board) {
        // 将2*3二维数组变为1*6一维数组
        vector<int> list;
        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 3; j++) {
                list.push_back(board[i][j]);
            }
        }
        int start = zip(list);
        // 终点状态[[1,2,3],[4,5,0]]，转化为整数为123450
        int target = 123450;
        // 用zip把list数组hash为一个整数存入queue作为起始状态，初始化dist[start] = 0
        q.push(start);
        dist[start] = 0;
        // 普通BFS搜索
        while (!q.empty()) {
            // 存储本次取出的整数并弹出
            int now = q.front();
            q.pop();
            // 拓展当前board中0的滑动位置
            // 将当前位置now还原为list数组，寻找当前0所处的位置，判断可行的移动位置
            auto a = unzip(now);
            int pos = getZeroIndex(a);
            // 判断边界越界问题
            if (pos != 0 && pos != 3) insert(pos, pos - 1, a, now); // 非最左侧可以左移
            if (pos != 2 && pos != 5) insert(pos, pos + 1, a, now); // 非最右侧可以右移
            if (pos >= 3) insert(pos, pos - 3, a, now); // 第二行可以上移
            if (pos < 3) insert(pos, pos + 3, a, now); // 第一行可以下移
            if (dist.find(target) != dist.end()) return dist[target]; // 当达到target，返回移动的次数
        }
        // 队列已空，无法达到target，返回-1
        return -1;
    }

    void insert(int pos, int newPos, vector<int>& a, int now) {
        swap(a[pos], a[newPos]);
        int next = zip(a);
        if (dist.find(next) == dist.end() || dist[next] > dist[now] + 1) {
            dist[next] = dist[now] + 1;
            q.push(next);
        }
        swap(a[pos], a[newPos]);
    }

    int getZeroIndex(vector<int>& a) {
        for (int i = 0; i < 6; i++){
            if (a[i] == 0) return i;
        }
        return -1;
    }

    int zip(vector<int>& a) {
        int res = 0;
        for (int i = 0; i < 6; i++) {
            res = res * 10 + a[i];
        }
        return res;
    }

    vector<int> unzip(int state) {
        vector<int> a(6, 0);
        for (int i = 5; i >= 0; i--) {
            a[i] = state % 10;
            state /= 10;
        }
        return a;
    }

    queue<int> q;
    unordered_map<int, int> dist; // 存入对应状态到达目标状态至少需要移动的次数，压缩后状态-最少移动次数

};
```
