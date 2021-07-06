```Java
// Java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        // 初始化结果序列数组sequence
        sequence = new ArrayList<Integer>();
        // 从root开始递归
        find(root);
        // 返回答案数组sequence
        return sequence;
    }

    // 递归函数find，中序遍历
    private void find(TreeNode root) {
        // 终止条件：root无子树
        if(root == null) return;
        // 遍历左子树
        find(root.left);
        sequence.add(root.val);
        // 遍历右子树
        find(root.right);
    }

    // 全局变量sequence，由所有函数体共享，在递归时进行修改和更新
    private List<Integer> sequence; 
}

```
