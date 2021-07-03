```Java
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
    public TreeNode invertTree(TreeNode root) {
    
        // 递归终止条件：root无子树
        if (root == null) return null;
        
        // 交换左右节点
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;

        // 翻转左边子树
        invertTree(root.left);
        // 翻转右边子树
        invertTree(root.right);

        // 返回翻转后的二叉树
        return root;
    }
}

```
