```C++
// C++
class TopVotedCandidate {
public:
    TopVotedCandidate(vector<int>& persons, vector<int>& times) {
        // 初始化计数数组count
        count = vector<int> (persons.size(), 0);
        // 初始化当前主导选举的候选人的编号记录数组
        currWinner = vector<int> (persons.size(), int());
        // copy一个times的时刻数组
        timeStamp = vector<int> (persons.size(), int());

        int maxCount = 1;
        int winner = persons[0];
        // 统计当前主导选举的候选人的编号记录数组
        for (int i = 0; i < persons.size(); i++) {
            // 累计count[persons[i]]
            timeStamp[i] = times[i];
            count[persons[i]]++;
            // 是 >= 而不是 >，保证当投票为平局时，最近获得投票的候选人获胜
            if (count[persons[i]] >= maxCount) { 
                winner = persons[i];
                maxCount = count[persons[i]];
            }
            // 从persons[0]到persons[i]，统计选票结果得到的目前主要选举的候选人编号
            currWinner[i] = winner;
        }
    }
    
    // 二分法确定t在times数组中的位置，以及当前的票数分布情况
    int q(int t) {
        // 上下界分别是times数组的头尾元素
        int l = 0;
        int r = timeStamp.size() - 1;
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (timeStamp[mid] > t) r = mid;
            else if(timeStamp[mid] < t) l = mid + 1;
            else { // timeStamp[mid] = t，times数组中有于t相符的元素
                l = mid;
                break;
            }
        }
        // 如果timeStamp[l-1] < t < timeStamp[l]，l减一
        if (t < timeStamp[l]){
            l--;
            // 如果l减一后小于0（= -1），将l重置为0
            if (l < 0) l = 0;
        }
        // 查询函数返回值，在t时刻主导选择的候选人的编号
        return currWinner[l];
    }

private: 
    vector<int> currWinner;
    // copy一个times数组
    vector<int> timeStamp;
    vector<int> count;
};

/**
 * Your TopVotedCandidate object will be instantiated and called as such:
 * TopVotedCandidate* obj = new TopVotedCandidate(persons, times);
 * int param_1 = obj->q(t);
 */
```
