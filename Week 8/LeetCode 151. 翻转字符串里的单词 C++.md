```C++

class Solution {
public:
    string reverseWords(string s) {
        // 将字符串s全部翻转
        reverse(s.begin(), s.end());
        int left = 0;
        int right = s.size() - 1;
        // 去除字符串s首末尾的所有空格，并更新左右端点索引
        while (s[right] == ' ' && 0 <= right) right--;
        while(s[left] == ' ' && left < right) left++;
        // 从更新后的left端点开始，到更新后的right端点结束，翻转每个单词
        // 步长为每个单词的长度
        for (int start = left; start <= right; ){
            // 确定每个单词的start和end
            while (s[start] == ' ' && start <= right) start++;
            int end = start;
            while (s[end] != ' ' && end <= right) end++;
            // 翻转单词
            reverse(s.begin() + start, s.begin() + end);
            // cout << s << endl;
            // 更新为下一个单词的start和end
            start = end;
        }
        // 翻转后单词间应当仅用一个空格分隔，去除中间的多余空格
        int newStart = left;
        for (int i = left; i <= right; i++){
            if (s[i] == ' ' && s[i - 1] == ' ') continue;
            s[newStart] = s[i];
            newStart++;
        }
        // 遍历后的newStart是字符串中单词的末尾位置，left是开始位置
        return s.substr(left, newStart - left);
    }
};

```
