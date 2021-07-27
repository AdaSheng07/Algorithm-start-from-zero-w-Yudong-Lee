```C++
// 方法一：动态规划，搜索方向自上而下，Top-down
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        vector<vector<int>> path (n, vector<int>(n, 0));
        path[0][0] = triangle[0][0];
        for (int i = 1; i < n; i++) {
            path[i][0] = path[i - 1][0] + triangle[i][0];
            for (int j = 1; j < triangle[i].size() - 1; j++){
                path[i][j] = min(path[i - 1][j], path[i - 1][j - 1]) + triangle[i][j];
            }
            // j = triangle[i].size() - 1 = i
            path[i][i] = path[i - 1][i - 1] + triangle[i][i];
        }
        return *min_element(path[n - 1].begin(), path[n - 1].end());
    }
};
```

```C++
// 方法二：动态规划，搜索方向自下而上，Bottom-up
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        vector<vector<int>> path (n + 1, vector<int>(n + 1, 0));
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j < triangle[i].size(); j++){
                path[i][j] = min(path[i + 1][j], path[i + 1][j + 1]) + triangle[i][j];
            }
        }
        return path[0][0];
    }
};
```

```C++
// 方法三：在方法二基础上对结果path内存进行优化
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        vector<int> path (n + 1, 0);
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j < triangle[i].size(); j++){
                path[j] = min(path[j], path[j + 1]) + triangle[i][j];
            }
        }
        return path[0];
    }
};
```

