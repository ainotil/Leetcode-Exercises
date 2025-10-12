# 代码随想录算法训练营 Day 17
530. 二叉搜索树的最小绝对差 | 501. 二叉搜索树中的众数 | 236. 二叉树的最近公共祖先

---

## 530. 二叉搜索树的最小绝对差
* 题目链接：[LeetCode 530 二叉搜索树的最小绝对差](https://leetcode.cn/problems/maximum-binary-tree)
* 文章链接：[代码随想录讲解 二叉搜索树的最小绝对差](https://programmercarl.com/0530.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E7%9A%84%E6%9C%80%E5%B0%8F%E7%BB%9D%E5%AF%B9%E5%B7%AE.html)

**看到题目的第一想法**  
上一题也是关于二叉搜索树的，知道使用中序遍历，就不难了。

**看完代码随想录之后的想法** 
无。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    int min_diff = INT_MAX;
    TreeNode* prev = nullptr;
    int getMinimumDifference(TreeNode* root) {
        doGetMinDiff(root);
        return min_diff;
    }

    void doGetMinDiff(TreeNode* root) {
        if (root == nullptr) {
            return;
        }

        getMinimumDifference(root->left);
        if (prev != nullptr) {
            min_diff = min(root->val - prev->val, min_diff);
        }
        prev = root;
        getMinimumDifference(root->right);
    }
};
```

## 501. 二叉搜索树中的众数
* 题目链接：[LeetCode 501 二叉搜索树中的众数](https://leetcode.cn/problems/find-mode-in-binary-search-tree/)
* 文章链接：[代码随想录讲解 二叉搜索树中的众数](https://programmercarl.com/0501.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E4%BC%97%E6%95%B0.html)

**看到题目的第一想法**  
上一题也是关于二叉搜索树的，知道使用中序遍历，就不难了。

**看完代码随想录之后的想法** 
无。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    vector<int> res;
    int count = 0;
    int maxCount = 0;
    TreeNode* prev = nullptr;
    vector<int> findMode(TreeNode* root) {
        doFindMode(root);
        return res;
    }

    void doFindMode(TreeNode* root) {
        if (root == nullptr) {
            return;
        }

        doFindMode(root->left);

        if (prev == nullptr) {
            count = 1;
        } else if (prev->val == root->val) {
            count += 1;
        } else {
            count = 1;
        }
        prev = root;
        if (count == maxCount) {
            res.push_back(root->val);
        } else if (count > maxCount) {
            maxCount = count;
            res.clear();
            res.push_back(root->val);
        }
        
        doFindMode(root->right);
    }
};
```

## 236. 二叉树的最近公共祖先
* 题目链接：[LeetCode 236 二叉树的最近公共祖先](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-tree/)
* 文章链接：[代码随想录讲解 二叉树的最近公共祖先](https://programmercarl.com/0236.%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E6%9C%80%E8%BF%91%E5%85%AC%E5%85%B1%E7%A5%96%E5%85%88.html)

**看到题目的第一想法**  
有点难，虽然知道可以后序遍历去处理哪个节点有没有出现过p和q两个子树，但是不知道怎么处理。

**看完代码随想录之后的想法** 
对于回溯的顺序更明白了，感觉画图后更清晰。

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

        if (root == p || root == q) {
            return root;
        }

        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if (left != nullptr && right != nullptr) {
            return root;
        } else if (left != nullptr) {
            return left;
        } else {
            return right;
        }
    }
};
```