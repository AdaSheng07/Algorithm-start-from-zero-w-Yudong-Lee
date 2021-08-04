```C++
class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        int n = edges.size();
        // 初始化father数组，推入元素0～n，此时所有father[i] = i
        for (int i = 0; i <= n; i++) {
            father.push_back(i);
        }
        for (auto& edge: edges){
            // 如果edge[0]与edge[1]所在不同集合，合并
            if (find(edge[0]) != find(edge[1])) {
                unionSet(edge[0], edge[1]);
                // 检查合并集合后的father数组
                // cout<<"father["<<edge[0]<<"]="<<father[edge[0]]<<"father["<< edge[1]<<"]="<<father[edge[1]];
            }
            // 当edge[0]与edge[1]已经在同一组，说明添加此条edge会有环，返回edge
            else return edge;
        }
        return {};
    }

private:
    vector<int> father;

    // 合并集合
    void unionSet(int i, int j){
        int x = find(i);
        int y = find(j);
        if (x != y) father[y] = x;
    }

    // 查询组合的代表，元素x在哪一组
    int find(int x){
        if (x == father[x]) return x;
        return father[x] = find(father[x]);
    }
};
```
