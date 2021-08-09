```C++

class Solution {
public:
    int lengthOfLastWord(string s) {
        int length = 0;
        // 从后向前遍历
        int i = s.size() - 1;
        while (i >= 0) {
            // 忽略字符串末尾的空格
            if (s[i] == ' ' && length == 0) {
                i--;
            }
            // 确定最后一个单词的开头位置（空格），返回最后一个单词的长度
            else if (s[i] == ' ' && length > 0){
                return length;
            }
            // 遍历位置不是空格，单词长度加一
            else {
                length++;
                i--;
            }
        }
        return length;
    }
};

```
