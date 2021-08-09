```C++

class Solution {
public:
    int firstUniqChar(string s) {
        // 建立hashmap，alphabet存储s中字符的出现频数
        unordered_map<char, int> alphabet;
        for (char ch : s) alphabet[ch]++;
        // 在alphabet中寻找频数为1的第一个字符key并返回在原string中的索引
        for (int i = 0; i < s.size(); i++){
            if (alphabet[s[i]] == 1){
                return i;
            }
        }
        // 如果不存在，返回-1
        return -1;
    }
};

```
