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
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return build(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1);
    }

    TreeNode* build(vector<int>& preorder, int l1, int r1, 
                    vector<int>& inorder, int l2, int r2){
        if (l1 > r1) return nullptr;
        TreeNode* root = new TreeNode(preorder[l1]);
        int mid = l2;
        while (root->val != inorder[mid]) mid++;
        int leftSize = mid - l2;
        int rightSize = r2 - mid; 
        root->left = build(preorder, l1 + 1, l1 + leftSize, inorder, l2, mid - 1);
        root->right = build(preorder, l1 + leftSize + 1, r1, inorder, mid + 1, r2);
        return root; 
    }
    
};
```
