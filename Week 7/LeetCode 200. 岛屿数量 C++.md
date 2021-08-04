```C++
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        // 初始化father，将grid中元素从0～(m*n-1)标记，所有元素的father指向自己
        for (int i = 0; i < m * n; i++) {
            father.push_back(i);
        }
        /* 遍历grid，遍历方向是向右和向下:*/
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++){
                if (grid[i][j] == '1') {
                    // 是陆地，合并组，组成岛屿
                    unionSet(i, j, grid);
                }
                // 如果grid[i][j]=0，将father数组对应索引位置的值置为-1
                else father[(i * n) + j] = -1;
            }
        }
        int ans = 0;
        // 统计：岛屿数量 = father中元素的根数量
        for (int i = 0; i < m * n; i++) {
            if (father[i] == i) ans++;
        }
        return ans;
    }

private:

    vector<int> father;

    void unionSet(int i, int j, vector<vector<char>>& grid) {
        int n = grid[0].size();
        int k = (i * n) + j;
        // i=0且j=0时，father[0] = 0
        if (i == 0 && j == 0) father[k] = find(k);
        /* 判断：如果grid[i][j]为1，
                其左边/上边的元素也为1，
                而且它与其左边/上边元素不在同一组，
                将其father置为其左边/上边元素所在组的代表，递归，合并组*/
        if (j >= 1 && grid[i][j - 1] == '1' && find(k) != find(k - 1)) father[find(k)] = find(k - 1);
        if (i >= 1 && grid[i - 1][j] == '1' && find(k) != find(k - n)) father[find(k)] = find(k - n);
    }

    int find(int x){
        if (father[x] == x) return x;
        return father[x] = find(father[x]);
    }
};
```
