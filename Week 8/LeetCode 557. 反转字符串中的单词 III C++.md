```C++

// 是LeetCode 151题的easy版子问题，不需要处理冗余空格问题，单词在字符串中的相对位置也不改变，仅对每个单词分别实现翻转

class Solution {
public:
    string reverseWords(string s) {
        // 分割字符串string中的所有单词，分别翻转
        // 在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格
        for (int start = 0; start < s.size(); ) {
            while (s[start] == ' ' && start < s.size()) start++;
            int end = start;
            while (s[end] != ' ' && end < s.size()) end++;
            reverse(s.begin() + start, s.begin() + end);
            start = end;
        }
        return s;
    }
};

```
