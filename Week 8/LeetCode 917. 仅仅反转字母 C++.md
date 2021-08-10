```C++

class Solution {
public:
    string reverseOnlyLetters(string s) {
        for (int i = 0, j = s.size() - 1; i < j; i++, j--) {
            // 双指针从头(i)尾(j)开始判断字符串中字符是否是字母
            // 如果s[i]不是字母，i向后移一位
            while ((!isalpha(s[i])) && i < s.size() - 1) i++;
            // 如果s[j]不是字母，j向前移一位
            while ((!isalpha(s[j])) && j > 0) j--;
            // 当s中所有字符都不是字母时，跳出循环，返回s本身，不需要翻转
            if (i > j) break;
            // 如果s[i]和s[j]都是字母，两者交换位置
            swap(s[i], s[j]);
        }
        // 返回已更新/不需更新的字符串s
        return s;
    }
};

```
