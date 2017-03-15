## [144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/#/solutions)
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

## [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)
*  第二版，标准dfs，而且注意用res.size()判断什么时候结束

```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        dfs(root, res, 0);
        return res;
    }
public:
    void dfs(TreeNode* root, vector<vector<int>>& res, int depth){
        if(root == NULL) return;
        if(res.size() == depth){
            res.push_back(vector<int>());
        }
        
        res[depth].push_back(root->val);
        dfs(root->left, res, depth+1);
        dfs(root->right, res, depth+1);
    }
};
```

## [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/#/solutions)
*  递归方法，注意对调之前要保存临时信息，因为对调之后right的值已经，不能直接用它

```C++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root == NULL) return NULL;
        TreeNode* tmp = root->right;
        root->right = invertTree(root->left);
        root->left = invertTree(tmp);
        
        return root;
    }
};
```

* 非递归的方法，也是用stack

```C++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        stack<TreeNode*> stack;
        stack.push(root);
        TreeNode* p = NULL;
        
        while(!stack.empty()){
            p = stack.top();
            stack.pop();
            if(p){
                stack.push(p->left); //先进left还是right没影响
                stack.push(p->right);
                swap(p->left, p->right);
            }
        }
        
        return root;
    }
};

```

