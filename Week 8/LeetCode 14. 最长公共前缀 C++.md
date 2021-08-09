```C++
// 采用分治方法，对strs中所有字符串进行横向扫描，每遍历一个新的字符串，更新一次最长公共前缀prefix，最坏时间复杂度为O(m * n)

class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        // 特判：strs中只有一个字符串时，返回它本身
        if (strs.size() == 1) return strs[0];
        // 初始化公共前缀prefix
        string prefix = strs[0];
        // 最长公共前缀可由str中所有字符串两两比较得到
        for (auto str : strs){
            // 特判：strs中如果有空字符串，不存在公共前缀，返回空字符串
            if (str.size() == 0) return "";
            // 调用compare函数，求两字符串的公共前缀
            prefix = compare(prefix, str);
        }
        return prefix;
    }

    string compare(string str1, string str2) {
        // str1与str2的最长公共前缀长度是两者长度的最小值
        int lengthMin = min(str1.size(), str2.size());
        int index = 0;
        while (str1[index] == str2[index] && index < lengthMin){
            index++;
        }
        // 跳出while-loop时的index减一是最长公共前缀的末尾位置，字符串长度为index
        return str1.substr(0, index);
    }
};

```
