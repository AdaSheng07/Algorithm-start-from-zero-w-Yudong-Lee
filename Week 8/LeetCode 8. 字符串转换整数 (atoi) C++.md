```C++

class Solution {
public:
    int myAtoi(string s) {
        int index = 0;
        // 整体框架1: 丢弃无用的前导空格
        while (s[index] == ' ' && index < s.size()) index++; 
        // 整体框架2: 检查正负号
        int sign = 1;
        if ((s[index] == '-' || s[index] == '+') && index < s.size()) {
            if (s[index] == '-') sign = -1;
            index++;
        }
        // 整体框架3: 处理数字，将数字转换为整数
        int val = 0;
        // 整体框架4: 遇到非数字字符，终止转换，如果都是数字，转换后返回结果
        while (s[index] >= '0' && s[index] <= '9' && index < s.size()) {
            // 细节：整数超过int32整数范围，需要截断
            if (val > (2147483647 - (s[index] - '0')) / 10) {
                if (sign == -1) return -2147483648;
                else return 2147483647;
            }
            val = val * 10 + (s[index] - '0');
            index++;
        }
        return val * sign;
    }
};

```
