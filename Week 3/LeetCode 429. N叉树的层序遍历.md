```C++
// C++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        vector<vector<int>> sequence;
        queue<pair<Node*, int>> q;
        q.push(make_pair(root, 0));
        while (q.empty() == false) {
            // 取出队头
            Node* node = q.front().first;
            int depth = q.front().second;
            // 队头推出
            q.pop();
            // 终止条件
            if (node == nullptr) break;
            // 避免越界
            if (sequence.size() <= depth) {
                sequence.push_back({});
            }
            sequence[depth].push_back(node->val);
            // 扩展一层
            for (Node* child : node->children){
                q.push(make_pair(child, depth + 1));
            }
        }
        return sequence;
    }
};


```
