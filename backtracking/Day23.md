# 代码随想录算法训练营 Day 23   
491. 非递减子序列 | 46. 全排列 | 47. 全排列II
---

## 491. 非递减子序列
* 题目链接：[LeetCode 491. 非递减子序列](https://leetcode.cn/problems/non-decreasing-subsequences/)
* 文章链接：[代码随想录讲解 非递减子序列](https://programmercarl.com/0491.%E9%80%92%E5%A2%9E%E5%AD%90%E5%BA%8F%E5%88%97.html)

**看到题目的第一想法**    
不太会做，之前做过树枝上的去重，也就是深度上去重。但这个是层上的去重，也就是广度去重。       

**看完代码随想录之后的想法**    
为什么这道题是要用层上去重，因为这道题是不能乱排序的，所以不同顺序排序的元素是不同的结果。只是这道题要递增顺序而已，从而排除了不同顺序排序的可能。  
层去重，确保同一层里，相同数字只尝试一次，避免重复展开相同子树。避免同一层中（即同一父节点下）重复尝试相同数字。 
树枝去重，确保同一路径中，不因为跳过前一个重复元素而重复选择下一个。如果同一个数前面没被选，你不能在当前这条路径上再次选它的复制版本。  
主要是排序和没排序的区别。    

**实现过程中遇到的困难**  
C++里`set`的函数用法。
   
---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> tmp;
    vector<vector<int>> findSubsequences(vector<int>& nums) {
        backtracking(nums, 0);
        return res;
    }

    void backtracking(vector<int> nums, int start) {
        if (tmp.size() > 1) {
            res.push_back(tmp);
        }

        unordered_set<int> used;
        for (int i = start; i < nums.size(); i++) {
            if ((tmp.size() > 0 && nums[i] < tmp.back()) || used.find(nums[i]) != used.end()) {
                continue;
            }
            
            tmp.push_back(nums[i]);
            used.insert(nums[i]);
            backtracking(nums, i + 1);
            tmp.pop_back();
        }
    }   
};
```

## 46. 全排列
* 题目链接：[LeetCode 46. 全排列](https://leetcode.cn/problems/permutations)
* 文章链接：[代码随想录讲解 全排列](https://programmercarl.com/0046.%E5%85%A8%E6%8E%92%E5%88%97.html)

**看到题目的第一想法**  
没想到要用`curr_using`数组做标记。  

**看完代码随想录之后的想法** 
主要是如果当前遍历过，就不能加入数组了，所以使用`curr_using`。      

**实现过程中遇到的困难**  
无   

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> tmp;
    vector<vector<int>> permute(vector<int>& nums) {
        vector<int> curr_using(nums.size(), 0);
        backtracking(nums, curr_using);
        return res;
    }

    void backtracking(vector<int>& nums, vector<int> curr_using) {
        if (tmp.size() == nums.size()) {
            res.push_back(tmp);
            return;
        }

        for (int i = 0; i < nums.size(); i++) {
            if (curr_using[i] == 1) {
                continue;
            }
            tmp.push_back(nums[i]);
            curr_using[i] = 1;
            backtracking(nums, curr_using);
            curr_using[i] = 0;
            tmp.pop_back();
        }
    }
};
```

## 47. 全排列II
* 题目链接：[LeetCode 47. 全排列II](https://leetcode.cn/problems/permutations-ii)
* 文章链接：[代码随想录讲解 全排列II](https://programmercarl.com/0047.%E5%85%A8%E6%8E%92%E5%88%97II.html)

**看到题目的第一想法**  
主要是树枝去重+层去重。  

**看完代码随想录之后的想法** 
无。      

**实现过程中遇到的困难**  
无   

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> tmp;
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<int> curr_using(nums.size(), 0);
        sort(nums.begin(), nums.end());
        backtracking(nums, curr_using);
        return res;
    }

    void backtracking(vector<int>& nums, vector<int> curr_using) {
        if (tmp.size() == nums.size()) {
            res.push_back(tmp);
            return;
        }

        unordered_set<int> used;
        for (int i = 0; i < nums.size(); i++) {
            if (curr_using[i] == 1 || used.find(nums[i]) != used.end()) {
                continue;
            }
            tmp.push_back(nums[i]);
            curr_using[i] = 1;
            used.insert(nums[i]);
            backtracking(nums,curr_using);
            tmp.pop_back();
            curr_using[i] = 0;
        }
    }
};
```