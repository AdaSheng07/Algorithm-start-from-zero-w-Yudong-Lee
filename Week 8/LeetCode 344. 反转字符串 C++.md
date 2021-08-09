```C++

class Solution {
public:
    void reverseString(vector<char>& s) {
        // 利用需要互换位置的s[i]与s[n-i-1]字符之间的差值delta进行推算
        int delta;
        for (int i = 0; i < (s.size()/2); i++){
            delta = s[s.size() - 1 - i] - s[i];
            // 先更新s[n-i-1]，再更新s[i]
            s[s.size() - 1 - i] = s[i];            
            s[i] = s[i] + delta;
        }
    }
};

```
