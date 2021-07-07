```C++
// C++
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
    // 总课程数量numCourses设为n
    n = numCourses;
    // 初始化出边数组edges为n个空数组
    edges = vector<vector<int>> (n, vector<int>());
    // 初始化入度数组inDegree为n个0
    inDegree = vector<int> (n, 0);
    // 根据输入所给的preresuisites中ai与bi的关系，遍历所有先修关系后加边
    // prerequisites中每一组先修关系为一对长度为2的数组[ai, bi]，表示bi是ai的先修课，在有向图中以bi->ai表示
    // 加边模板
    for (vector<int> pre: prerequisites) {
        int ai = pre[0];
        int bi = pre[1];
        addEdges(bi, ai);
    }
    return topsort() == n;
    }

private:
    // 加边addEdges函数模板
    // 在edges中x元素的加边数组末尾加入y，构成x->y的新边
    void addEdges (int x, int y) {
        edges[x].push_back(y);
        // 同时统计y的入度
        inDegree[y]++;
    }

    // 基于BFS实现拓扑排序
    int topsort() {
        // 统计遍历过后学过的课程数量，初始化learned
        int learned = 0;
        // 拓扑排序利用队列，初始化队列q
        queue<int> q;
        // 找到inDegree中入度为0的点，先推入队列中
        for (int i = 0; i < n; i ++) {
            if (inDegree[i] == 0) q.push(i);
        }
        // 当队列q不为空时，执行BFS
        while (!q.empty()){
        // 取队列q的队头，保存之后推出队列q，说明队头代表的这门课已经学过了
        int x = q.front();
        q.pop();
        // 每pop一个队头，说明一节课已经学过了
        learned++;
        // 考虑队头的所有出边，出边指向的点代表此门课可以学
        for (int y : edges[x]) { // 找到x->y的边，因为x已经学过了，y可以学，y的入度减一
            inDegree[y]--;
            // 判断：当y的入度也为0时，说明y也没有先修课了，y也已经学过了，将y推入队列q，继续递归
            if (inDegree[y] == 0) q.push(y);
        }
        }
        // 当队列q为空时，递归终止，返回已经学过的课程数量
        return learned;
    }

    int n;
    // 设置出边数组
    vector<vector<int>> edges;
    // 设置入度数组
    vector<int> inDegree;


};

```
