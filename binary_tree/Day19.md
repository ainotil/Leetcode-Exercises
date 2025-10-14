# 代码随想录算法训练营 Day 19
669.修剪二叉搜索树 | 108.将有序数组转换为二叉搜索树 | 538. 把二叉搜索树转换为累加树

---

## 669. 修剪二叉搜索树
* 题目链接：[LeetCode 669 修剪二叉搜索树](https://leetcode.cn/problems/trim-a-binary-search-tree)
* 文章链接：[代码随想录讲解 修剪二叉搜索树](https://programmercarl.com/0669.%E4%BF%AE%E5%89%AA%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.html)

**看到题目的第一想法**  
能写出大概结构，但是写不对。

**看完代码随想录之后的想法** 
其实就是跳过不在范围内的节点。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        if (root == nullptr) {
            return nullptr;
        }
        if (root->val < low) {
            return trimBST(root->right, low, high);
        } else if (root->val > high) {
            return trimBST(root->left, low, high);
        }

        root->left = trimBST(root->left, low, high);
        root->right = trimBST(root->right, low, high);
        return root;
    }
};
```

## 108. 将有序数组转换为二叉搜索树
* 题目链接：[LeetCode 108 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/trim-a-binary-search-tree)
* 文章链接：[代码随想录讲解 将有序数组转换为二叉搜索树](https://programmercarl.com/0108.%E5%B0%86%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E8%BD%AC%E6%8D%A2%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.html)

**看到题目的第一想法**  
比较简单，一遍过。主要是前序遍历的方式，因为利用有序数组的特性，左子树肯定比右子树小，数组前面的肯定比后面的小。

**看完代码随想录之后的想法** 
无。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return doSortedArrayToBST(nums, 0, nums.size());
    }

    TreeNode* doSortedArrayToBST(vector<int>& nums, int start, int end) {
        if (start == end) {
            return nullptr;
        }
        TreeNode* root = new TreeNode(nums[(start + end) / 2]);
        root->left = doSortedArrayToBST(nums, start, (start + end) / 2);
        root->right = doSortedArrayToBST(nums, (start + end) / 2 + 1, end);
        return root;
    }
};
```

## 538. 把二叉搜索树转换为累加树
* 题目链接：[LeetCode 538 把二叉搜索树转换为累加树](https://leetcode.cn/problems/convert-bst-to-greater-tree/)
* 文章链接：[代码随想录讲解 把二叉搜索树转换为累加树](https://programmercarl.com/0538.%E6%8A%8A%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E8%BD%AC%E6%8D%A2%E4%B8%BA%E7%B4%AF%E5%8A%A0%E6%A0%91.html)

**看到题目的第一想法**  
比较简单，一遍过。理解遍历顺序，右中左。

**看完代码随想录之后的想法** 
无。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    int sum = 0;
    TreeNode* convertBST(TreeNode* root) {
        doConvertBST(root);
        return root;
    }
    
    void doConvertBST(TreeNode* root) {
        if (root == nullptr) {
            return;
        }

        doConvertBST(root->right);
        sum += root->val;
        root->val = sum;
        doConvertBST(root->left);
    }
};
```