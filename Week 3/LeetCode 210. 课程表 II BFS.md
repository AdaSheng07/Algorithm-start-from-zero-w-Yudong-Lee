```C++
// C++
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        // 初始化
        n = numCourses;
        edges = vector<vector<int>> (n, vector<int>());
        inDegree =  vector<int> (n, 0);
        // 根据输入所给的preresuisites中ai与bi的关系，遍历所有先修关系后加边
        // prerequisites中每一组先修关系为一对长度为2的数组[ai, bi]，表示bi是ai的先修课，在有向图中以bi->ai表示
        // 加边模板
        for (vector<int> pre : prerequisites) {
            int ai = pre[0];
            int bi = pre[1];
            addEdge(bi, ai);
        }

        // 基于BFS的拓扑排序
        // BFS基于队列，初始化队列q
        queue<int> q;
        // 将所有入度等于0的点推入队列，它们没有先修课，是搜索的起点
        for (int i = 0; i < n; i ++) {
            if (inDegree[i] == 0) q.push(i);
        }
        // 当队列不为空时，递归执行BFS遍历
        while (!q.empty()){
            // 取队头，保存队头点x方便遍历队头的出边，将队头x推出，代表队头这门课x已经学了
            int x = q.front();
            q.pop();
            // 在学习路径的最后加入这门课x
            learnPath.push_back(x);
            // 遍历此队头x的出边，因为这门课x已经学了，此队头指向的点y代表的课程可以学
            for (int y : edges[x]) { // 找到x->y的边，因为x已经学过了，y可以学，y的入度减一
                inDegree[y]--; 
                // 判断：当y的入度也为0时，说明y这门课也已经学完了，推入队列q，继续递归
                if (inDegree[y] == 0) q.push(y);
            }
        }
        // BFS遍历结束后，判断是否学完了所有课程，如果没有，说明有环，不可能完成所有课程，返回空数组
        if (learnPath.size() != n) return {};
        // 所有课程都学完了，返回课程学习路径
        return learnPath;
    }

private: 
    // 加边函数addEdge
    void addEdge (int x, int y) {
        edges[x].push_back(y);
        // 同时统计y的入读
        inDegree[y]++;
    }

    int n;
    // 出边数组存储
    vector<vector<int>> edges;
    // 每个点的入度存储
    vector<int> inDegree;
    // 课程学习路径存储，全局变量
    vector<int> learnPath;
};
```
