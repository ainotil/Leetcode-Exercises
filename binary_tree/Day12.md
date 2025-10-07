# 代码随想录算法训练营 Day 12
(144, 145, 94) 递归遍历 | (144, 145, 94) 迭代遍历 | (144, 145, 94) 统一遍历 | 102. 二叉树的层序遍历

---

## 二叉树的递归遍历
* 题目链接：[LeetCode 144 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)
* 题目链接：[LeetCode 145 二叉树的后序遍历](https://leetcode.cn/problems/binary-tree-postorder-traversal/)
* 题目链接：[LeetCode 94 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)
* 文章链接：[代码随想录讲解 递归遍历](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html)

**看到题目的第一想法**  
比较简单。

**看完代码随想录之后的想法** 
和我想的差不多，但是看完讲解思路更清晰了一些。 

**实现过程中遇到的困难**  
无。

---

### 代码
```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        doPreorderTraversal(root, &res);
        return res;
    }

    void doPreorderTraversal(TreeNode* root, vector<int> *res) {
        if (root == nullptr) {
            return;
        }

        res->push_back(root->val);
        doPreorderTraversal(root->left, res);
        doPreorderTraversal(root->right, res);
    }
};
```

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        doPostorderTraversal(root, &res);
        return res;
    }

    void doPostorderTraversal(TreeNode* root, vector<int>* res) {
        if (root == nullptr) {
            return;
        }

        doPostorderTraversal(root->left, res);
        doPostorderTraversal(root->right, res);
        res->push_back(root->val);
    }
};
```

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        doInorderTraversal(root, &res);
        return res;
    }

    void doInorderTraversal(TreeNode* root, vector<int> *res) {
        if (root == nullptr) {
            return;
        }

        doInorderTraversal(root->left, res);
        res->push_back(root->val);
        doInorderTraversal(root->right, res);
    }
};
```

## 二叉树的递归遍历
* 题目链接：[LeetCode 144 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)
* 题目链接：[LeetCode 145 二叉树的后序遍历](https://leetcode.cn/problems/binary-tree-postorder-traversal/)
* 题目链接：[LeetCode 94 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)
* 文章链接：[代码随想录讲解 递归遍历](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%80%92%E5%BD%92%E9%81%8D%E5%8E%86.html)

**看到题目的第一想法**  
比较简单。

**看完代码随想录之后的想法** 
和我想的差不多，但是看完讲解思路更清晰了一些。 

**实现过程中遇到的困难**  
理解栈中左子节点，右子节点，和根节点的遍历顺序。

---

### 代码
```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        if (root == nullptr) {
            return res;
        }

        stack<TreeNode*> s;
        s.push(root);

        while (!s.empty()) {
            TreeNode* curr = s.top();
            res.push_back(curr->val);
            s.pop();
            if (curr->right != nullptr) {
                s.push(curr->right);
            }
            if (curr->left != nullptr) {
                s.push(curr->left);
            }
        }

        return res;
    }
};
```

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        if (root == nullptr) {
            return res;
        }

        stack<TreeNode*> s;
        s.push(root);

        while (!s.empty()) {
            TreeNode* curr = s.top();
            res.push_back(curr->val);
            s.pop();
            if (curr->left != nullptr) {
                s.push(curr->left);
            }
            if (curr->right != nullptr) {
                s.push(curr->right);
            }
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if (root == nullptr) {
            return res;
        }

        stack<TreeNode*> s;
        TreeNode* curr = root;

        while (curr != nullptr || !s.empty()) {
            if (curr != nullptr) {
                s.push(curr);
                curr = curr->left;
            } else {
                curr = s.top();
                s.pop();
                res.push_back(curr->val);
                curr = curr->right;
            }
        }

        return res;
    }
};
```

## 二叉树的统一迭代
* 题目链接：[LeetCode 144 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)
* 题目链接：[LeetCode 145 二叉树的后序遍历](https://leetcode.cn/problems/binary-tree-postorder-traversal/)
* 题目链接：[LeetCode 94 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)
* 文章链接：[代码随想录讲解 统一迭代](https://programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E7%BB%9F%E4%B8%80%E8%BF%AD%E4%BB%A3%E6%B3%95.html)

**看到题目的第一想法**  
没什么想法，不了解什么是统一迭代。

**看完代码随想录之后的想法** 
理解了怎么写，主要是之前掌握了中序的遍历迭代。

**实现过程中遇到的困难**  
理解栈中左子节点，右子节点，和根节点的遍历顺序。

---

### 代码
```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode*> s;
        if (root != nullptr) {
            s.push(root);
        }

        TreeNode* curr;
    
        while (!s.empty()) {
            curr = s.top();
            if (curr != nullptr) {
                s.pop();
                if (curr->right != nullptr) {
                    s.push(curr->right);
                }
                if (curr->left != nullptr) {
                    s.push(curr->left);
                }
                s.push(curr);
                s.push(nullptr);
            } else {
                s.pop();
                curr = s.top();
                s.pop();
                res.push_back(curr->val);
            }
        }

        return res;
    }
};
```

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode*> s;
        if (root != nullptr) {
            s.push(root);
        }
        TreeNode* curr = nullptr;
        while (!s.empty()) {
            curr = s.top();
            if (curr != nullptr) {
                s.pop();
                s.push(curr);
                s.push(nullptr);
                if (curr->right != nullptr) {
                    s.push(curr->right);
                }
                if (curr->left != nullptr) {
                    s.push(curr->left);
                }
            } else {
                s.pop();
                curr = s.top();
                s.pop();
                res.push_back(curr->val);
            }
            
        }
        
        return res;
    }
};
```

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode*> s;
        if (root != nullptr) {
            s.push(root);
        }
        
        while(!s.empty()) {
            TreeNode* curr = s.top();
            if (curr != nullptr) {
                s.pop();
                if (curr->right != nullptr) {
                    s.push(curr->right);
                }
                s.push(curr);
                s.push(nullptr);
                if (curr->left != nullptr) {
                    s.push(curr->left);
                }
            } else {
                s.pop();
                curr = s.top();
                s.pop();
                res.push_back(curr->val);
            }
        }

        return res;
    }
};
```

## 102 - 二叉树的层序遍历
* 题目链接：[LeetCode 102 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/description/)
* 文章链接：[代码随想录讲解 统一迭代](https://programmercarl.com/0102.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86.html)

**看到题目的第一想法**  
想到了使用队列这点，以及怎么遍历二叉树。但是不知道怎么加入数组，感觉思路有点不太清晰。

**看完代码随想录之后的想法** 
思路清晰了，不太难。

**实现过程中遇到的困难**  
无。

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        queue<TreeNode*> q;
        int size = 0;
        if (root != nullptr) {
            q.push(root);
        }

        while(!q.empty()) {
            int size = q.size();
            vector<int> layer;
            while (size--) {
                TreeNode* curr = q.front();
                layer.push_back(curr->val);
                if (curr->left != nullptr) {
                    q.push(curr->left);
                }
                if (curr->right != nullptr) {
                    q.push(curr->right);
                }
                q.pop();
            }
            res.push_back(layer);
        }
        return res;
    }
};
```