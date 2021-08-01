```C++
class Trie {

private:
    struct Node {
        int count;
        unordered_map<char, Node*> child;
        Node(): count(0) {}
    };
    Node* root;

    bool solve(string s, bool prefix_match, bool insert_if_not_exist) {
        Node* curr = root;
        for (auto ch : s) {
            if (curr->child.find(ch) == curr->child.end()) {
                if (insert_if_not_exist) curr->child[ch] = new Node();
                else return false;
            }
            curr = curr->child[ch];
        }
        if (insert_if_not_exist) curr->count++;
        if (prefix_match) return true;
        return curr->count > 0;
    }

public:

    /** Initialize your data structure here. */
    Trie() {
        root = new Node();
    }

    /** Inserts a word into the trie. */
    void insert(string word) {
        solve(word, false, true);
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        return solve(word, false, false);
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        return solve(prefix, true, false);
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```
