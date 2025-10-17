# 代码随想录算法训练营 Day 22   
93. 复原IP地址 | 78. 子集

---

## 93. 复原IP地址
* 题目链接：[LeetCode 93 复原IP地址](https://leetcode.cn/problems/restore-ip-addresses/)
* 文章链接：[代码随想录讲解 复原IP地址](https://programmercarl.com/0093.%E5%A4%8D%E5%8E%9FIP%E5%9C%B0%E5%9D%80.html)

**看到题目的第一想法**    
大概知道怎么写，回溯，分割，判断是不是IP地址。    

**看完代码随想录之后的想法**    
和我的细节处理的不一样，思路一致，我暂且保留我的。  

**实现过程中遇到的困难**  
判断是不是IP地址这里挺繁琐的，改了好久。尤其最后要把`.`加回`tmp`是真的没想到，这也是回溯的过程，要保证`tmp`是完好的。  

---

### 代码
```cpp
class Solution {
public:
    vector<string> res;
    string tmp = "";
    int count = 0;
    vector<string> restoreIpAddresses(string s) {
        backtracking(s, 0);
        return res;
    }

    void backtracking(string s, int start) {
        if (start == s.size() && count == 4) {
            tmp.pop_back();
            res.push_back(tmp);
            tmp += '.'; 
            return;
        }

        for (int i = start; i < s.size(); i++) {
            string sub = s.substr(start, i - start + 1);
            if (sub.size() > 3) {
                return; 
            } else if (sub.size() > 1 && sub[0] == '0') {
                return;
            } else if (count == 4) {
                return;
            } else if (stoi(sub) > 255) {
                return;
            }

            count += 1;
            tmp += sub + '.';
            backtracking(s, i + 1);
            tmp.resize(tmp.size() - sub.size() - 1);
            count -= 1;
        }
    }
};
```

## 78. 子集
* 题目链接：[LeetCode 78. 子集](https://leetcode.cn/problems/subsets/)
* 文章链接：[代码随想录讲解 子集](https://programmercarl.com/0078.%E5%AD%90%E9%9B%86.html)

**看到题目的第一想法**    
大概知道怎么写，比较简单的一题。     

**看完代码随想录之后的想法**    
思路一致，但是代码随想录的解法更清晰，我原本的写法还是基于对组合的理解。

**实现过程中遇到的困难**  
无。    

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> tmp;
    vector<vector<int>> subsets(vector<int>& nums) {
        backtracking(nums, 0);
        return res;
    }

    void backtracking(vector<int>& nums, int start) {
        res.push_back(tmp);

        for (int i = start; i < nums.size(); i++) {
            tmp.push_back(nums[i]);
            backtracking(nums, i + 1);
            tmp.pop_back();
        }
    }
};
```

## 90. 子集II
* 题目链接：[LeetCode 90. 子集II](https://leetcode.cn/problems/subsets-ii/)
* 文章链接：[代码随想录讲解 子集II](https://programmercarl.com/0090.%E5%AD%90%E9%9B%86II.html)

**看到题目的第一想法**    
能看出来是组合II和子集。但是组合II的解法忘记用`curr_using`了，复习了一下。     

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
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        vector<int> curr_using(nums.size(), 0);
        sort(nums.begin(), nums.end());
        back_tracking(nums, 0, curr_using);
        return res;
    }

    void back_tracking(vector<int>& nums, int start, vector<int> curr_using) {
        res.push_back(tmp);

        for (int i = start; i < nums.size(); i++) {
            if (i != 0 && nums[i] == nums[i - 1] && curr_using[i - 1] != 1) {
                continue;
            }
            tmp.push_back(nums[i]);
            curr_using[i] = 1;
            back_tracking(nums, i + 1, curr_using);
            tmp.pop_back();
            curr_using[i] = 0;
        }
    }
};
```