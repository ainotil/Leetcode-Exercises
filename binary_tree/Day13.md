# 代码随想录算法训练营 Day 12
226.翻转二叉树 | 101. 对称二叉树 | 104. 二叉树的最大深度

---

## 226 - 翻转二叉树
* 题目链接：[LeetCode 226 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree)
* 文章链接：[代码随想录讲解 翻转二叉树](https://programmercarl.com/0226.%E7%BF%BB%E8%BD%AC%E4%BA%8C%E5%8F%89%E6%A0%91.html)

**看到题目的第一想法**  
比较简单，一遍过了。

**看完代码随想录之后的想法** 
无

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

## 101 - 对称二叉树
* 题目链接：[LeetCode 101 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)
* 文章链接：[代码随想录讲解 对称二叉树](https://programmercarl.com/0101.%E5%AF%B9%E7%A7%B0%E4%BA%8C%E5%8F%89%E6%A0%91.html)

**看到题目的第一想法**  
考虑到了要对比子节点的内外两种情况的问题，但是没有想到可以在参数里直接放左右子节点进行比较，所以没做出来。  

**看完代码随想录之后的想法** 
了解了遍历顺序，思路更清晰了，看完讲解就写出来了。  

**实现过程中遇到的困难**  
无。   

---

### 代码
```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return compare(root->left, root->right);
    }

    bool compare(TreeNode* left, TreeNode* right) {
        if (left == nullptr && right != nullptr) {
            return false;
        } else if (left != nullptr && right == nullptr) {
            return false;
        } else if (left == nullptr && right == nullptr) {
            return true;
        } else if (left != nullptr && right != nullptr && left->val != right->val) {
            return false;
        } else {
            return compare(left->left, right->right) && compare(left->right, right->left);
        }
    }
};
```

## 104 - 二叉树的最大深度
* 题目链接：[LeetCode 104 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)
* 文章链接：[代码随想录讲解 二叉树的最大深度](https://programmercarl.com/0104.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%A4%A7%E6%B7%B1%E5%BA%A6.html)

**看到题目的第一想法**  
这题做过，一遍对了

**看完代码随想录之后的想法** 
理解了高度和深度的区别。  

**实现过程中遇到的困难**  
无。   

---

### 代码
```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }

        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```

## 104 - 二叉树的最小深度
* 题目链接：[LeetCode 111 二叉树的最小深度](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)
* 文章链接：[代码随想录讲解 二叉树的最小深度](https://programmercarl.com/0111.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E6%B7%B1%E5%BA%A6.html)

**看到题目的第一想法**  
做不太对。

**看完代码随想录之后的想法** 
还是加深了对深度的理解，深度需要找的是最靠上的叶子节点。所以当一个节点只有一个子节点的时候，如果用之前的解法，就会截止到当前节点。但是当前节点不是真正的叶子节点。   

**实现过程中遇到的困难**  
无。   

---

### 代码
```cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }

        if (root->left != nullptr && root->right != nullptr) {
            return min(minDepth(root->left), minDepth(root->right)) + 1;
        } else if (root->left != nullptr) {
            return minDepth(root->left) + 1;
        } else if (root->right != nullptr) {
            return minDepth(root->right) + 1;
        } else {
            return 1;
        }

    }
};
```