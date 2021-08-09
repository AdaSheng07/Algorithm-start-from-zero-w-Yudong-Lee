```C++

class Solution {
public:
    string reverseStr(string s, int k) {
        // 每2k个字符反转前k个字符，遍历字符串s时i以2k为步长
        for (int i = 0; i < s.size(); i += (2 * k)) {
            // 只要剩余字符大于k个，就能把前k个字符反转
            if (s.size() >= i + k) {
                reverse(s, i, i + k - 1);
            }
            // 如果剩余字符少于k个，将剩余所有字符反转
            else reverse(s, i, s.size() - 1);
        }
        return s;
    }

    // 反转字符函数模板与344题双指针实现相同
    void reverse(string& s, int left, int right) {
        for (int i = left, j = right; i < j; i++, j--){
            swap(s[i], s[j]);
        }
    }

};

```
