```C++
// C++
class Solution {
public:
    int robotSim(vector<int>& commands, vector<vector<int>>& obstacles) {
        // 初始化
        int x = 0;
        int y = 0;
        int dir = 0; // 开始时面向北方
        int ans = 0;

        // 生成存放障碍物位置（二元数组）的无序集合blockers，便于访问查询
        // 方案1，改为string
        unordered_set<string> blockers; 
        // 如果用方案2，改为：
        unordered_set<long long> blockers;
        for (auto& obstacle : obstacles){
            blockers.insert(calcHash(obstacle[0], obstacle[1])); // 将hash函数计算后的key作为blockers中的索引
        }

        // 问题重点2: 利用方向数组指导(x, y)的移动方向
        /* 向北移动1时，x不变，y加一
           向东移动1时，x加一，y不变
           向南移动1时，x不变，y减一
           向西移动1时，x减一，y不变
        */
        // 按照北、东、南、西的方位存储x方向和y方向的位置变化
        int dx[4] = {0, 1, 0, -1};
        int dy[4] = {1, 0, -1, 0};

        // 基于commands对(x, y)进行操作
        for (int cmd : commands){
            // 如果cmd > 0，(x, y)向前移动cmd个单位长度
            if (cmd > 0) {
                for (int i = 0; i < cmd; i++){
                    // 计算(x, y)的下一步位置
                    int next_x = x + dx[dir];
                    int next_y = y + dy[dir];
                    // 如果(x, y)的下一步是障碍物位置，那么在这一次cmd下(x, y)位置不变，等待下一次cmd
                    if (blockers.find(calcHash(next_x, next_y)) != blockers.end()) break;
                    // 如果(x, y)的下一步不是障碍物位置，更新(x, y)位置，进行下一步操作
                    x = next_x;
                    y = next_y;
                    // 返回从原点到机器人所有经过的路径点（坐标为整数）的最大欧式距离的平方
                    ans = max(ans, x * x + y * y);
                }
            // 如果cmd = -2，向左转 90 度
            // 方向变化为北->西->南->东->北
            // 对应的dic在方向数组中索引变化为0->3->2->1->0
            }else if(cmd == -2) {
                dir = (dir - 1 + 4) % 4;
            }else
            // 如果cmd = -1，向右转90度
            // 方向变化为北->东->南->西->北
            // 对应的dic在方向数组中索引变化为0->1->2->3->0
            dir = (dir + 1) % 4;
        }
        return ans;
    }

// 问题重点1：判断障碍
// 两个方案：利用hash函数将二元数组转换为string或者大整数，供unordered_set寻找是否有blocker
// 方案1: 转变为string
private:
    string calcHash(int x, int y){
        return to_string(x) + "," + to_string(y); 
    }

// 方案2: 转变为大整数long long
// 将(x, y)看作进制数的第1和第0位，防止为负先平移坐标系再换算
private:
    long long calcHash(int x, int y){
        return (x + 30000) * 60000ll + y + 30000;
    }

};
```
