#### ACSII码对照表

![image](https://user-images.githubusercontent.com/86143164/128653995-c0fbe965-9dd4-4b75-87a8-466cc4b198c2.png)


```C++
// 方法一：通过ASCII码对照表知，大小写字母的ASCII码值相差32

class Solution {
public:
    string toLowerCase(string s) {
        for (int i = 0; i < s.size(); i++) {
            if (s[i] >= 'A' && s[i] <= 'Z') {
                s[i] += 32;
            }
        }
        return s;
    }
};

```

```C++
// 方法二：利用位运算

/*
大写变小写、小写变大写：字符 ^= 32;
大写变小写、小写变小写：字符 |= 32;
大写变大写、小写变大写：字符 &= 33;
*/

class Solution {
public:
    string toLowerCase(string s) {
        for (int i = 0; i < s.size(); i++) {
            if (s[i] >= 65 && s[i] <= 90) {
                s[i] |= 32;
            }
        }
        return s;
    }
};

```
