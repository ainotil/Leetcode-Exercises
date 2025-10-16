# 代码随想录算法训练营 Day 21   
39. 组合总和 | 40. 组合总和II | 131. 分割回文串

---

## 39. 组合总和
* 题目链接：[LeetCode 39 组合总和](https://leetcode.cn/problems/combination-sum/)
* 文章链接：[代码随想录讲解 组合总和](https://programmercarl.com/0039.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8C.html)

**看到题目的第一想法**    
看到提示就是`startIndex`不同后就很简单了。

**看完代码随想录之后的想法**    
无。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> tmp;
    int sum = 0;
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        backtracking(candidates, target, 0);
        return res;
    }

    void backtracking(vector<int>& candidates, int target, int start) {
        if (sum > target) {
            return;
        } else if (sum == target) {
            res.push_back(tmp);
            return;
        }

        for (int i = start; i < candidates.size(); i++) {
            tmp.push_back(candidates[i]);
            sum += candidates[i];
            backtracking(candidates, target, i);
            tmp.pop_back();
            sum -= candidates[i];
        }
    }
};
```

## 40. 组合总和II
* 题目链接：[LeetCode 40 组合总和II](https://leetcode.cn/problems/combination-sum-ii/description/)
* 文章链接：[代码随想录讲解 组合总和II](https://programmercarl.com/0040.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CII.html)

**看到题目的第一想法**  
不太会去重。

**看完代码随想录之后的想法**    
首先需要理解要在哪里去重，重复的结果是怎么生成的。  
在回溯的过程中，在从一个元素`a`以及其之后要搜索的时候，如果其后面有相同的元素`b`，就会必定有重复的结果。因为假设`a`和`b`能和`c`组成所求和，那么如果`a`以一层全部的可能被遍历过了，`b`以另一层在搜寻可能时，遇到`c`时就会产生重复的结果，因为`a`和`c`已经被加入过了。  
所以为了让遍历`b`时排除掉`a`已经被遍历过的情况，我们先排序原数组，这时`a`和`b`挨着的。再使用`using`记录，如果`using[a] == 1`，指被遍历过，这里的被遍历过不是层上，而是枝上，代表我们还在找`a`的所有可能。而`using[a] == 0`时，才代表`a`已经被完全遍历完了，因为我们开始搜索`b`为第一个元素时，`using[a] == 0`。   
其实这也是个在回溯中跳过相同元素的一种方式。  

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> res; 
    vector<int> tmp;
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<int> using(candidates.size(), 0);
        sort(candidates.begin(), candidates.end());
        backtracking(candidates, target, 0, 0, using);
        return res;
    }

    void backtracking(vector<int>& candidates, int target, int sum, int start, vector<int> using) {
        if (sum > target) {
            return;
        } else if (sum == target) {
            res.push_back(tmp);
            return;
        }

        for (int i = start; i < candidates.size(); i++) {
            if (i != 0 && candidates[i] == candidates[i-1] && using[i-1] == 0) {
                continue;
            }
            tmp.push_back(candidates[i]);
            sum += candidates[i];
            using[i] = 1;
            backtracking(candidates, target, sum, i + 1, using);
            using[i] = 0;
            tmp.pop_back();
            sum -= candidates[i];
        }
    }
};
```

## 131. 分割回文串
* 题目链接：[LeetCode 131 分割回文串](https://leetcode.cn/problems/combination-sum-ii/description/)
* 文章链接：[代码随想录讲解 分割回文串](https://programmercarl.com/0131.%E5%88%86%E5%89%B2%E5%9B%9E%E6%96%87%E4%B8%B2.html)

**看到题目的第一想法**  
大概能想出解法的结构，但是不会分割。  
分割其实就是组合的一种变体，用start作为分割的起点，用i作为分割的终点。  
如果当前分割的一部分，存在不是回文串的子字符串，就跳过当前这种分割方式。  

**看完代码随想录之后的想法**    
  

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    vector<vector<string>> res;
    vector<string> tmp;
    vector<vector<string>> partition(string s) {
        backtracking(s, 0);
        return res;
    }

    bool isPalindrome(string s, int start, int end) {
        for (int i = start, j = end; i <= j; i++, j--) {
            if (s[i] != s[j]) {
                return false;
            }
        }
        return true;
    }

    void backtracking(string s, int start) {
        if (start == s.size()) {
            res.push_back(tmp);
            return;
        }
        for (int i = start; i < s.size(); i++) {
            if (isPalindrome(s, start, i)) {
                tmp.push_back(s.substr(start, i - start + 1));
            } else {
                continue;
            }
            backtracking(s, i + 1);
            tmp.pop_back();
        }
    }
};
```