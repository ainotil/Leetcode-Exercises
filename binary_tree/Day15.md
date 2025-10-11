# 代码随想录算法训练营 Day 14
513. 找树左下角的值 | 112.路经总和 
---

## 找树左下角的值
* 题目链接：[LeetCode 513 找树左下角的值](https://leetcode.cn/problems/find-bottom-left-tree-value/)
* 文章链接：[代码随想录讲解 找树左下角的值](https://programmercarl.com/0513.%E6%89%BE%E6%A0%91%E5%B7%A6%E4%B8%8B%E8%A7%92%E7%9A%84%E5%80%BC.html)

**看到题目的第一想法**  
想到了用层序遍历，递归不太明白。

**看完代码随想录之后的想法** 
理解了遍历的顺序。其实这道题不难，就是找最大深度第一个被遍历的叶子节点。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    int findBottomLeftValue(TreeNode* root) {
        int maxDepth = -1;
        int res = 0;
        doFindBottomLeftValue(root, 0, &maxDepth, &res);
        return res;
    }

    void doFindBottomLeftValue(TreeNode* root, int curr_depth, int *maxDepth, int *res) {
        if (root->left == nullptr && root->right == nullptr) {
            if (curr_depth > *maxDepth) {
                *res = root->val;
                *maxDepth = curr_depth;
            }
        }
        if (root->left != nullptr) {
            doFindBottomLeftValue(root->left, curr_depth + 1, maxDepth, res);
        } 
        if (root->right != nullptr) {
            doFindBottomLeftValue(root->right, curr_depth + 1, maxDepth, res);
        }
        
    }
};
```

## 路径总和
* 题目链接：[LeetCode 112 路径总和](https://leetcode.cn/problems/path-sum/)
* 文章链接：[代码随想录讲解 路径总和](https://programmercarl.com/0112.%E8%B7%AF%E5%BE%84%E6%80%BB%E5%92%8C.html)

**看到题目的第一想法**  
这道题挺难的，虽然看出规律了，但是细节处理不好，做不出来。

**看完代码随想录之后的想法** 
理解了切割数组，但是切割数组后代码的表现一般。就用了文章里说的索引法，但是让代码繁琐了许多，用了一点时间debug。   

**实现过程中遇到的困难**  
索引切割比较难，陷阱多。   

---

### 代码
```cpp
class Solution {
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if (inorder.size() == 0) {
            return nullptr;
        }
        return doBuildTree(inorder, postorder, 0, inorder.size(), 0, postorder.size());
    }

    TreeNode* doBuildTree(vector<int>& inorder, vector<int>& postorder, int inorder_s, int inorder_e, int postorder_s, int postorder_e) {
        if (postorder_e == postorder_s) {
            return nullptr;
        }
        TreeNode* root = new TreeNode(postorder[postorder_e - 1]);

        if (postorder_e == 1) {
            return root;
        }

        int i = inorder_s;
        for(; i < inorder_e ; i++) {
            if (inorder[i] == root->val) {
                break;
            }
        }

        int left_inorder_s = inorder_s;
        int left_inorder_e = i;
        int right_inorder_s = i + 1;
        int right_inorder_e = inorder_e;

        int left_postorder_s = postorder_s;
        int left_postorder_e = postorder_s + i - inorder_s;
        int right_postorder_s = postorder_s + i - inorder_s;
        int right_postorder_e = postorder_e - 1;

        root->left = doBuildTree(inorder, postorder, left_inorder_s, left_inorder_e, left_postorder_s, left_postorder_e);
        root->right = doBuildTree(inorder, postorder, right_inorder_s, right_inorder_e, right_postorder_s, right_postorder_e);

        return root;
    }
};
```
