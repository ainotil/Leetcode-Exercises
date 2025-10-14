# 代码随想录算法训练营 Day 18
235. 二叉搜索树的最近公共祖先 | 701. 二叉搜索树中的插入操作 | 450. 删除二叉搜索树中的节点

---

## 235. 二叉搜索树的最近公共祖先
* 题目链接：[LeetCode 235 二叉搜索树的最近公共祖先](https://leetcode.cn/problems/maximum-binary-tree)
* 文章链接：[代码随想录讲解 二叉搜索树的最近公共祖先](https://programmercarl.com/0530.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E7%BB%9D%E5%AF%B9%E5%B7%AE.html)

**看到题目的第一想法**  
不太会做，虽然看出二叉搜索树的规律，但是想不太明白。

**看完代码随想录之后的想法** 
二叉搜索树的特性理解了，当一个节点的值在两个节点之间时，这就是最近公共祖先。因为左子树的值必定都小于右子树，不存在次最近公共祖先的情况。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == nullptr) {
            return nullptr;
        }

        if ((p->val >= root->val && q->val <= root->val) || (p->val <= root->val && q->val >= root->val)) {
            return root;
        } else if (p->val >= root->val && q->val >= root->val) {
            return lowestCommonAncestor(root->right, p, q);
        } else {
            return lowestCommonAncestor(root->left, p, q);
        }
    }
};
```

## 701. 二叉搜索树中的插入操作
* 题目链接：[LeetCode 701 二叉搜索树中的插入操作](https://leetcode.cn/problems/insert-into-a-binary-search-tree/)
* 文章链接：[代码随想录讲解 二叉搜索树的最近公共祖先](https://programmercarl.com/0701.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E6%8F%92%E5%85%A5%E6%93%8D%E4%BD%9C.html)

**看到题目的第一想法**  
比较简单。  

**看完代码随想录之后的想法**    
和我做的一样，只不过用了一个上个节点的操作。

**实现过程中遇到的困难**  
C++指针。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        doInsertIntoBST(&root, val);
        return root;
    }

    void doInsertIntoBST(TreeNode** root, int val) {
        if (*root == nullptr) {
            *root = new TreeNode(val);
            return;
        }

        if ((*root)->val > val) {
            if ((*root)->left == nullptr) {
                (*root)->left = new TreeNode(val);
                return;
            } else {
                insertIntoBST((*root)->left, val);
            }
        } else  {
            if ((*root)->right == nullptr) {
                (*root)->right = new TreeNode(val);
                return;
            } else {
                insertIntoBST((*root)->right, val);
            }
        }
    }
};
```

## 450. 删除二叉搜索树中的节点
* 题目链接：[LeetCode 450 删除二叉搜索树中的节点](https://leetcode.cn/problems/delete-node-in-a-bst/description/)
* 文章链接：[代码随想录讲解 删除二叉搜索树中的节点](https://programmercarl.com/0450.%E5%88%A0%E9%99%A4%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html)

**看到题目的第一想法**  
不会！  

**看完代码随想录之后的想法** 
总结出五种情况：   
1. 没找到要删的节点：直接返回树。   
2. 叶子节点左右为空：直接删除当前节点。    
3. 要删的节点左为空，右不为空：将当前节点替换成右子树。    
4. 要删的节点左不为空，右为空： 将当前节点替换成左子树。   
5. 要删的节点左不为空，右不为空：将当前节点的左子树接到右子树的最左叶节点上，再将当前节点替换成右子树。  

**实现过程中遇到的困难**  
无。

---

### 代码
```cpp
class Solution {
public:

    TreeNode* deleteNode(TreeNode* root, int key) {
        if (root == nullptr) {
            return nullptr;
        }

        if (root->val == key) {
            if (root->left == nullptr && root->right == nullptr) {
                delete root;
                return nullptr;
            } else if (root->left != nullptr && root->right == nullptr) {
                TreeNode* tmp = root;
                root = root->left;
                delete tmp;
                return root;
            } else if (root->left == nullptr && root->right != nullptr) {
                TreeNode* tmp = root;
                root = root->right;
                delete tmp;
                return root;
            } else {
                TreeNode* tmp = root->right;
                while (tmp->left != nullptr) {
                    tmp = tmp->left;
                }
                tmp->left = root->left;
                tmp = root;
                root = root->right;
                delete tmp;
                return root;
            }
        }
        root->left = deleteNode(root->left, key);
        root->right = deleteNode(root->right, key);
        return root;
    }
};
```