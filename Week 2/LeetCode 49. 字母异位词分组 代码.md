```Java
// Java
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {

        unordered_map<string, vector<string>> groupWords;
        vector<vector<string>> ans;

        for (auto& str : strs){
            string copy = str;
            sort(copy.begin(), copy.end());
            groupWords[copy].push_back(str);
        }

        for (auto pair : groupWords){
            ans.push_back(pair.second);
        }
        return ans;
    }
};
```
