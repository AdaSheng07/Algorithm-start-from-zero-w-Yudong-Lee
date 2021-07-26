```C++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int n = obstacleGrid.size(); 
        int m = obstacleGrid[0].size();
        vector<vector<int>> f (n, vector<int>(m, 0));
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (obstacleGrid[i][j] == 1) f[i][j] = 0;
                else if (i == 0 && j == 0) f[i][j] = 1;
                else if (i == 0) f[i][j] = f[i][j - 1];
                else if (j == 0) f[i][j] = f[i - 1][j];
                else f[i][j] = f[i - 1][j] + f[i][j - 1];
            }
        }
        return f[n -1][m -1];
    }
};
```
