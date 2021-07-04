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

    /*
    节点的左子树只包含小于当前节点的数。
    节点的右子树只包含大于当前节点的数。
    所有左子树和右子树自身必须也是二叉搜索树。
    */

class Solution {
    public boolean isValidBST(TreeNode root) {
        return check(root).isValid;
    }


    private class Info {
        public boolean isValid;
        public long minVal;
        public long maxVal;
    }
    

    private Info check(TreeNode root) {
        if (root == null) {
            Info info = new Info();
            info.isValid = true;
            info.minVal = Integer.MAX_VALUE + 1L;
            info.maxVal = Integer.MIN_VALUE - 1L;
            return info;
        }
        Info left = check(root.left);
        Info right = check(root.right);
        Info result = new Info();
        result.isValid = left.isValid && right.isValid 
            && left.maxVal < root.val && right.minVal > root.val;
        result.minVal = Math.min(Math.min(right.minVal, left.minVal), root.val);
        result.maxVal = Math.max(Math.max(right.maxVal, left.maxVal), root.val);
        return result;
    }
}











```
