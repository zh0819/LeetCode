# [236. 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)

```C++
class Solution {
public:
    TreeNode * sub_lowestCommonAncestor(TreeNode * root,TreeNode * p,TreeNode *q)
    {
        if(!root) return nullptr;
        if(root == p || root == q) return root;

        TreeNode * left = sub_lowestCommonAncestor(root->left,p,q);
        TreeNode * right =  sub_lowestCommonAncestor(root->right,p,q);

        if(left && right) return root;
        if(left && !right) return left;
        if(!left && right) return right;

        return nullptr;
    }
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root) return nullptr;
        return sub_lowestCommonAncestor(root,p,q);
    }
};
```

- 这道题和之前的递归不同，需要从底往上遍历，之前都是从上往下遍历
- 从底往上走需要用到后序遍历，例如求二叉树的最大深度（高度）
- 这道题还给了一个思考点就是前面的递归终止条件
  - 之前一直考虑的是为空则返回，一直考虑的时候遍历到叶子结点的下一层节点返回
  - 这道题的递归终止条件设置，可能使得到某一个子树根节点就会返回了
  - 所以不要惯性思维