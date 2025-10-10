# 代码随想录算法训练营 Day 14

---

## 平衡二叉树
* 题目链接：[LeetCode 110 平衡二叉树](https://leetcode.cn/problems/balanced-binary-tree/)
* 文章链接：[代码随想录讲解 平衡二叉树](https://programmercarl.com/0110.%E5%B9%B3%E8%A1%A1%E4%BA%8C%E5%8F%89%E6%A0%91.html)

**看到题目的第一想法**  
不太会做！

**看完代码随想录之后的想法** 
加深了对高度和深度的理解，高度是从下往上传，所以是后序遍历。而深度是从上往下传，所以是前序遍历。此题是求高度，所以要后序遍历，再加上`-1`的使用就可以解出来了。   

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        return (checkIsBalanced(root) != -1);
    }

    int checkIsBalanced(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }

        int left = checkIsBalanced(root->left);
        if (left == -1) {
            return -1;
        }
        int right = checkIsBalanced(root->right);
        if (right == -1) {
            return -1;
        }

        if (abs(right - left) > 1) {
            return -1;
        } else {
            return max(right, left) + 1;
        }
    }
};
```

## 二叉树的所有路径
* 题目链接：[LeetCode 257 二叉树的所有路径](https://leetcode.cn/problems/binary-tree-paths/)
* 文章链接：[代码随想录讲解 二叉树的所有路径](https://programmercarl.com/0257.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%89%80%E6%9C%89%E8%B7%AF%E5%BE%84.html)

**看到题目的第一想法**  
一遍做对了，但是消耗内存不好。

**看完代码随想录之后的想法** 
修改了一些小细节，消耗内存上来了。

**实现过程中遇到的困难**  
C++语法，指针那些。  

---

### 代码
```cpp
class Solution {
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> res;
        string path;
        if (root == nullptr) {
            return res;
        }
        doBinaryTreePaths(root, path, &res);
        return res;
    }

    void doBinaryTreePaths(TreeNode* root, string curr, vector<string> *res) {
        curr += to_string(root->val);
        if (root->left == nullptr && root->right == nullptr) {
            res->push_back(curr);
            return;
        }

        if (root->left != nullptr) {
            doBinaryTreePaths(root->left, curr + "->", res);
        }

        if (root->right != nullptr) {
            doBinaryTreePaths(root->right, curr + "->", res);
        }
    }
};
```

## 左子叶之和
* 题目链接：[LeetCode 404 左子叶之和](https://leetcode.cn/problems/sum-of-left-leaves/description/)
* 文章链接：[代码随想录讲解 左子叶之和](https://programmercarl.com/0404.%E5%B7%A6%E5%8F%B6%E5%AD%90%E4%B9%8B%E5%92%8C.html)

**看到题目的第一想法**  
挺简单的，一遍对了。

**看完代码随想录之后的想法** 
和我的做法不一样，加深理解吧。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        int res = 0;
        if (root == nullptr) {
            return res;
        }
        doSumOfLeftLeaves(root, false, &res);
        return res;
    }
    
    void doSumOfLeftLeaves(TreeNode *curr, bool isLeft, int *res) {
        if (curr->left == nullptr && curr->right == nullptr && isLeft) {
            *res += curr->val;
            return;
        } 

        if (curr->left != nullptr) {
            doSumOfLeftLeaves(curr->left, true, res);
        } 
        if (curr->right != nullptr) {
            doSumOfLeftLeaves(curr->right, false, res);
        }
    }
};
```

```cpp
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }
        if (root->left == nullptr && root->right == nullptr) {
            return 0;
        }

        int left = sumOfLeftLeaves(root->left);
        if (root->left != nullptr && root->left->left == nullptr && root->left->right == nullptr) {
            left = root->left->val;
        }

        int right = sumOfLeftLeaves(root->right);

        return left + right;
    }
};
```

## 完全二叉树的节点个数
* 题目链接：[LeetCode 222 完全二叉树的节点个数](https://leetcode.cn/problems/count-complete-tree-nodes)
* 文章链接：[代码随想录讲解 完全二叉树的节点个数](https://programmercarl.com/0222.%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%8A%82%E7%82%B9%E4%B8%AA%E6%95%B0.html)

**看到题目的第一想法**  
知道怎么判断是不是完全二叉树，但是不知道怎么实现。   

**看完代码随想录之后的想法** 
先判断是不是完全二叉树，如果是，直接返回深度。如果不是，再用传统的方法算。  

**实现过程中遇到的困难**  
无。   

---

### 代码
```cpp
class Solution {
public:
    int countNodes(TreeNode* root) {
        if (root == nullptr){
            return 0;
        }

        // 剪枝
        TreeNode* left = root->left;
        int left_depth = 0;
        while(left != nullptr) {
            left_depth += 1;
            left = left->left;
        }

        TreeNode* right = root->right;
        int right_depth = 0;
        while(right != nullptr) {
            right_depth += 1;
            right = right->right;
        }

        if (left_depth == right_depth) {
            return (2 << left_depth) - 1;
        } else {
            return countNodes(root->left) + countNodes(root->right) + 1;
        }

    }
};
```
