# 代码随想录算法训练营 Day 16
654. 最大二叉树 | 617. 合并二叉树 | 700. 二叉搜索树中的搜索 | 98. 验证二叉搜索树

---

## 654. 最大二叉树
* 题目链接：[LeetCode 654 最大二叉树](https://leetcode.cn/problems/maximum-binary-tree)
* 文章链接：[代码随想录讲解 最大二叉树](https://programmercarl.com/0654.%E6%9C%80%E5%A4%A7%E4%BA%8C%E5%8F%89%E6%A0%91.html)

**看到题目的第一想法**  
简单版本的从中序与后序遍历序列构造二叉树，昨天做过，竟然一遍过了。

**看完代码随想录之后的想法** 
无。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        return doConstruct(nums, 0, nums.size());
    }

    TreeNode* doConstruct(vector<int>& nums, int start, int end) {
        if (start - end == 0) {
            return nullptr;
        }

        int max = start;
        for (int i = start; i < end; i++) {
            if (nums[i] > nums[max]) {
                max = i;
            }
        }

        TreeNode* root = new TreeNode(nums[max]);
        root->left = doConstruct(nums, start, max);
        root->right = doConstruct(nums, max + 1, end);
        return root;
    }
};
```

## 617. 合并二叉树
* 题目链接：[LeetCode 617 合并二叉树](https://leetcode.cn/problems/merge-two-binary-trees)
* 文章链接：[代码随想录讲解 合并二叉树](https://programmercarl.com/0617.%E5%90%88%E5%B9%B6%E4%BA%8C%E5%8F%89%E6%A0%91.html)

**看到题目的第一想法**  
比较简单，一遍过，但是代码表现不太好。

**看完代码随想录之后的想法** 
终止条件更简洁了。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if (root1 == nullptr) {
            return root2;
        }
        if (root2 == nullptr) {
            return root1;
        }

        TreeNode* root = new TreeNode(root1->val + root2->val);
        root->left = mergeTrees(root1->left, root2->left);
        root->right = mergeTrees(root1->right, root2->right);
        return root;
    }

};
```

## 700. 二叉搜索树中的搜索
* 题目链接：[LeetCode 700 二叉搜索树中的搜索](https://leetcode.cn/problems/search-in-a-binary-search-tree/)
* 文章链接：[代码随想录讲解 二叉搜索树中的搜索](https://programmercarl.com/0700.%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E4%B8%AD%E7%9A%84%E6%90%9C%E7%B4%A2.html)

**看到题目的第一想法**  
比较简单，一遍过。

**看完代码随想录之后的想法** 
终止条件更简洁了。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if (root1 == nullptr) {
            return root2;
        }
        if (root2 == nullptr) {
            return root1;
        }

        TreeNode* root = new TreeNode(root1->val + root2->val);
        root->left = mergeTrees(root1->left, root2->left);
        root->right = mergeTrees(root1->right, root2->right);
        return root;
    }

};
```

## 98. 验证二叉搜索树
* 题目链接：[LeetCode 98 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree)
* 文章链接：[代码随想录讲解 验证二叉搜索树](https://programmercarl.com/0098.%E9%AA%8C%E8%AF%81%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.html)

**看到题目的第一想法**  
做不对。

**看完代码随想录之后的想法** 
理解了应该用中序遍历，从而以从小到大的顺序遍历后，就明白了。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if (root1 == nullptr) {
            return root2;
        }
        if (root2 == nullptr) {
            return root1;
        }

        TreeNode* root = new TreeNode(root1->val + root2->val);
        root->left = mergeTrees(root1->left, root2->left);
        root->right = mergeTrees(root1->right, root2->right);
        return root;
    }

};
``` 