```Java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<Integer> preorder(Node root) {
        // 初始化答案数组sequence
        sequence = new ArrayList<Integer> ();
        find(root);
        return sequence;
        
    }

    private void find(Node root) {
        // 终止条件
        if (root == null) return;
        // 从根开始
        sequence.add(root.val);
        // 循环递归root的所有子节点
        for (Node child : root.children) {
            find(child);
        }
    }

    private List<Integer> sequence;
}

```
