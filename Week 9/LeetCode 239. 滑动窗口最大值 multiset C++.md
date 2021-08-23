```C++

#include <set>

class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        vector<int> ans;
        multiset<int> window;
        int left = 0;
        int i = 0;
        while (i <= k + left - 1 && i < nums.size()) {
            window.insert(nums[i]);
            if (i == k + left - 1) {
                ans.push_back(*window.rbegin());
                window.erase(window.find(nums[left]));
                left++;
            }
            i++;
        }
        return ans;
    }
};

```
