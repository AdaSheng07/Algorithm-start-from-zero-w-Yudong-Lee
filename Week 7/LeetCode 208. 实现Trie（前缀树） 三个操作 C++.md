```C++
class Trie {

private:
    struct Node {
        int count;
        unordered_map<char, Node*> child;
        Node(): count(0) {}
    };
    Node* root;

public:

    /** Initialize your data structure here. */
    Trie() {
        root = new Node();
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        Node* curr = root;
        for (auto ch : word) {
            if (curr->child.find(ch) == curr->child.end()) {
                curr->child[ch] = new Node();
            }
            curr = curr->child[ch];
        }
        curr->count++;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        Node* curr = root;
        for (auto ch : word) {
            if (curr->child.find(ch) == curr->child.end()) {
                return false;
            }
            curr = curr->child[ch];
        }
        return curr->count > 0;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        Node* curr = root;
        for (auto ch : prefix) {
            if (curr->child.find(ch) == curr->child.end()) {
                return false;
            }
            curr = curr->child[ch];
        }
        return true;
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
