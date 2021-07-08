```C++
// C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        return build(inorder, 0, inorder.size() - 1, postorder, 0, postorder.size() - 1); 
    }

    TreeNode* build(vector<int>& inorder, int l1, int r1, 
                    vector<int>& postorder, int l2, int r2){
    if (l1 > r1) return nullptr; 
    // 根据后序遍历存储最后一个元素为root
    TreeNode* root = new TreeNode(postorder[r2]);
    // 在中序遍历中寻找root所在位置并存储索引mid
    int mid = l1;
    while (inorder[mid] != root->val) mid++;
    // 分别计算左子树与右子树的size
    int leftSize = mid - l1;
    // 右子树的size其实用不上
    // int rightSize = r1 - mid;
    // 递归左右子树，构造二叉树
    root->left = build(inorder, l1, mid - 1, postorder, l2, l2 + leftSize - 1);
    root->right = build(inorder, mid + 1, r1, postorder, l2 + leftSize, r2 - 1);
    return root;
    }

};


```
