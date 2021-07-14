```C++
// C++

// 利用优先队列
# include<queue>

// 设置堆结点，将推文的ID，即tweetID与时间点建立联系，时间点timeStamp是用于比较的关键码
struct Tweet{
    int tweetId;
    int timeStamp;
    Tweet *next;
    Tweet(int tweetId, int timeStamp) : tweetId(tweetId), timeStamp(timeStamp), next(nullptr) {}
};

// 比较函数，重载小于号，基于timeStamp进行Tweet发布时间的大小比较，需要返回最近的十条推特，所以是大根堆
bool operator < (const Tweet& a, const Tweet& b) {
    return a.timeStamp < b.timeStamp;
}

class Twitter {

// 设置需要维护的全局变量
private:
    // 每个用户的userId与关注的人的userId的集合之间建立映射
    unordered_map<int, set<int>> userIdfolloweeId;
    // 每个用户的userId与其所发Tweet（包括tweetId与timeStamp）之间建立映射
    unordered_map<int, Tweet*> userIdTweet;
    // 变化的时间点
    int timePoint;

public:
    /** Initialize your data structure here. */
    Twitter() {
        // 初始化时间点
        timePoint = 0;
    }
    
    /** Compose a new tweet. */
    void postTweet(int userId, int tweetId) {
        // 建立一条新的推特
        Tweet* tweet = new Tweet(tweetId, timePoint++);
        // 如果哈希表userIdTweet中没有此userId，新建这条userId->tweet的记录
        if (userIdTweet.find(userId) == userIdTweet.end()) userIdTweet[userId] = tweet;
        else{
            // 否则，将新加入的这条记录作为头节点，新的tweet指向此user前一条tweet
            tweet -> next = userIdTweet.find(userId)->second;
            // 并且将哈希表userIdTweet更新
            userIdTweet[userId] = tweet;
        }

    }
    
    /** Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent. */
    vector<int> getNewsFeed(int userId) {
        vector<int> ans;
        // 优先队列q通过小于号比较heap
        priority_queue<Tweet*> q;
        // 如果有userId用户自己发的推特，加入优先队列q
        if (userIdTweet.find(userId) != userIdTweet.end()) {
            q.push(userIdTweet.find(userId)->second);
        }
        // 如果有，找到userId用户关注的其他用户
        if (userIdfolloweeId.find(userId) != userIdfolloweeId.end()){
            // 对关注的人的userId的集合进行遍历，寻找他们的推特
            for (auto followee : userIdfolloweeId[userId]) {
                // 如果关注的人有发布推特，加入优先队列q
                if (userIdTweet.find(followee) != userIdTweet.end()) q.push(userIdTweet.find(followee)->second);
            }
        }
        // 检索此用户最近的十条推文
        int count = 1;
        // 循环终止条件：已经检索十条推文 或 优先队列已为空
        while (count <= 10 && !q.empty()) {
            // 取出10个指针指向的最近十条推文
            Tweet* t = q.top();
            // 将取出的最新一条推特的tweetId放入答案数组ans
            ans.push_back(t->tweetId);
            // 将已记录的这条最新推特弹出
            q.pop();
            // 如果这条推特结点后仍有推特，将其推入优先队列
            if (t->next != nullptr) q.push(t->next);
            count ++;
        }
        return ans;
    }
    
    /** Follower follows a followee. If the operation is invalid, it should be a no-op. */
    void follow(int followerId, int followeeId) {
        // 当followerId等于followeeId时，操作无效
        if (followerId == followeeId) return;
        // 当userIdfolloweeId中不含有followerId时，新增这条记录
        if (userIdfolloweeId.find(followerId) == userIdfolloweeId.end()) {
            userIdfolloweeId[followerId] = {followeeId};
        } else {
            // 当userIdfolloweeId中含有followerId时，在其对应的followee集合中加入新followeeId
            userIdfolloweeId[followerId].insert(followeeId);
        }
    }
    
    /** Follower unfollows a followee. If the operation is invalid, it should be a no-op. */
    void unfollow(int followerId, int followeeId) {
        // 当followerId等于followeeId时，操作无效
        if (followerId == followeeId) return;
        // 当userIdfolloweeId的userId中确认有followerId，且userIdfolloweeId的followeeId确认有此followeeId，去除此映射
        if (userIdfolloweeId.find(followerId) != userIdfolloweeId.end()
                && userIdfolloweeId[followerId].find(followeeId) != userIdfolloweeId[followerId].end()){
                    userIdfolloweeId[followerId].erase(followeeId);
                }
    }
};

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter* obj = new Twitter();
 * obj->postTweet(userId,tweetId);
 * vector<int> param_2 = obj->getNewsFeed(userId);
 * obj->follow(followerId,followeeId);
 * obj->unfollow(followerId,followeeId);
 */
```
