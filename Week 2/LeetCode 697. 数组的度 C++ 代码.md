``` C++
class Solution {
public:
    int findShortestSubArray(vector<int>& nums) {

        // 以hashmap将数组元素映射到一个数组
        /* 这里在vector中记录每个元素出现位置的最左和最右
           整数是每个元素在nums中的出现次数*/
        unordered_map<int, vector<int>> map;
        // 初始化数组的度
        int degree = 0;

        // count每个元素的出现次数，并记录元素在数组nums中出现位置的最左和最右
        for (int i = 0; i < nums.size(); i++){
            // 如果元素是第一次被统计，find后返回尾指针，计数为1，左右位置均为i
            if (map.find(nums[i]) == map.end()){
                map[nums[i]] = {1, i, i};
            } else {
                // 如果元素中已经有此元素，count加一，更新元素出现的最右端位置为当前index i
                map[nums[i]][0] ++;
                map[nums[i]][2] = i;
            }
            // 数组的度：数组里任一元素出现频数的最大值
            // 每一次nums[i]遍历后的map[nums[i]][0]，即当前nums[i]出现次数，与degree比较后取大
            // 边遍历边更新，遍历结束后得到nums数组的度
            degree = max(degree, map[nums[i]][0]);
            // cout << i << ":" << map[nums[i]][0]<< "," << map[nums[i]][1] << "," << map[nums[i]][2] << endl;
        }
        // cout << degree << endl;

        // 初始化最短连续子数组长度，最长为nums的长度
        int lenMin = nums.size();
        // 对map中的统计次数进行遍历
        for (auto& pair : map){
            // cout << pair.second[1] << "," << pair.second[2] << endl;
            // 找出与nums的度相同的pair，计算pair的对应的元素的左右端位置距离
            if(pair.second[0] == degree){
                // 所有满足条件的pair中，左右端距离的最小值就是最短连续子数组的长度
                lenMin = min(lenMin, pair.second[2] - pair.second[1] + 1);
            }
        }
        return lenMin;
    }
};
```
