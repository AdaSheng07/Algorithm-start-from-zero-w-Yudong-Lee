```C++
// 方法一：暴力，时间复杂度O(m * n)，因S和J最多含有50个字母所以可行

class Solution {
public:
    int numJewelsInStones(string jewels, string stones) {
        int cnt = 0;
        for (int j = 0; j < jewels.size(); j++){
            for (int i = 0; i < stones.size(); i++){
                if (stones[i] == jewels[j]) cnt++;
            }
        }
        return cnt;
    }
};

```

```C++
// 方法二：在方法一基础上优化，利用hashset将时间复杂度简化为O(m + n)

class Solution {
public:
    int numJewelsInStones(string jewels, string stones) {
        // J中字符不重复，将J中字符分别存储在无序集合jewel中
        unordered_set<char> jewel;
        for (char j : jewels){
            jewel.insert(j);
        }
        int cnt = 0;
        // 对字符串S遍历，如果集合jewel中存在字符s，计数加一
        for (char s : stones){
            if (jewel.find(s) != jewel.end()) cnt++;
        }
        return cnt;
    }
};

```
