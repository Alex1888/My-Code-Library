# [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/#/solutions)
```C++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> v;
        if(!root) return v;
        
        stack<TreeNode*> stack;
        TreeNode* p = root;
        
        while(p != NULL || !stack.empty()){
            if(p != NULL){
                v.push_back(p->val); // print befor go to children
                stack.push(p);// 一路向左 
                p = p->left;
            }else{
                TreeNode* topnode = stack.top();
                stack.pop();
                p = topnode->right; // 向左到底了，从栈顶取出节点(位于p的上一层)，它的right作为子树的root，
            }
        }
        
        return v;
    }
};
```

## [94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/#/description)
*  递归做法

```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        inorderTrv(root, result);
        return result;
    }
    
public:
   void inorderTrv(TreeNode* root, vector<int>& re){
       if(root != NULL){
           inorderTrv(root->left, re);
           re.push_back(root->val);
           inorderTrv(root->right, re);
       }
   }
};
```

*  非递归，one stack方法

```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> v;
        if(!root) return v;
        
        stack<TreeNode*> stk;
        TreeNode* pCurrent = root;
        
        // 注意root不需要先入栈
        while(pCurrent!= NULL || !stk.empty()){
            if(pCurrent != NULL){
                stk.push(pCurrent);
                pCurrent = pCurrent->left;
            }
            else
            {
                TreeNode* topnode = stk.top();
                v.push_back(topnode->val); // print after all left node
                stk.pop();
                pCurrent = topnode->right;
            }
        }
        
        return v;
    }
};
```
# [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/#/solutions)
```C++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> v;
        if(!root) return v;
        
        stack<TreeNode*> stack;
        TreeNode* p = root;
        
        while(p != NULL || !stack.empty()){
            if(p != NULL){
                v.push_back(p->val); // print befor go to children
                stack.push(p);// 一路向左 
                p = p->left;
            }else{
                TreeNode* topnode = stack.top();
                stack.pop();
                p = topnode->right; // 向左到底了，从栈顶取出节点(位于p的上一层)，它的right作为子树的root，
            }
        }
        
        return v;
    }
};
```
