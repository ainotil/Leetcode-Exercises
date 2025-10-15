# 代码随想录算法训练营 Day 20  
77.组合 | 216. 组合总和 III

---

## 77. 组合
* 题目链接：[LeetCode 77 组合](https://leetcode.cn/problems/combinations/)
* 文章链接：[代码随想录讲解 组合](https://programmercarl.com/0077.%E7%BB%84%E5%90%88.html)

**看到题目的第一想法**  
想到了用一套一套的循环，但是做不出来。

**看完代码随想录之后的想法** 
少了弹出这一步，明白了回溯的道理，处理完当前元素后应该弹出，再处理下一个元素可能的组合。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> tmp;
    vector<vector<int>> combine(int n, int k) {
        backtracking(n, k, 1);
        return res;
    }

    void backtracking(int n, int k, int start) {
        if (tmp.size() == k) {
            res.push_back(tmp);
            return;
        }

        for (int i = start; i <= n; i++) {
            tmp.push_back(i);
            backtracking(n, k, i + 1);
            tmp.pop_back();
        }
    }
};
```

## 216. 组合总和III
* 题目链接：[216. 组合总和III](https://leetcode.cn/problems/combinations/)
* 文章链接：[代码随想录讲解 组合总和III](https://programmercarl.com/0216.%E7%BB%84%E5%90%88%E6%80%BB%E5%92%8CIII.html)

**看到题目的第一想法**  
和上一题差不多，就是多了一个求和的条件。

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
    int sum = 0;
    vector<int> tmp;
    vector<vector<int>> combinationSum3(int k, int n) {
        backtracking(k, n, 1);
        return res;
    }

    void backtracking(int k, int n, int start) {
        if (tmp.size() == k) {
            if (sum == n) {
                res.push_back(tmp);
            }
            return;
        }

        for (int i = start; i <= 9; i++) {
            tmp.push_back(i);
            sum += i;
            backtracking(k, n, i + 1);
            tmp.pop_back();
            sum -= i;
        }

    }
};
```

## 17. 电话号码的字母组合
* 题目链接：[LeetCode 17 电话号码的字母组合](https://leetcode.cn/problems/letter-combinations-of-a-phone-number/)
* 文章链接：[代码随想录讲解 电话号码的字母组合](https://programmercarl.com/0017.%E7%94%B5%E8%AF%9D%E5%8F%B7%E7%A0%81%E7%9A%84%E5%AD%97%E6%AF%8D%E7%BB%84%E5%90%88.html)

**看到题目的第一想法**  
有点麻烦的一题，但是不难，做出来了，但是代码不是很简洁，而且空间不是很理想。

**看完代码随想录之后的想法** 
使用lettermap，可以让代码整洁很多。

**实现过程中遇到的困难**  
无。  

---

### 代码
```cpp
class Solution {
private:
    const string letterMap[10] = {
        "", // 0
        "", // 1
        "abc", // 2
        "def", // 3
        "ghi", // 4
        "jkl", // 5
        "mno", // 6
        "pqrs", // 7
        "tuv", // 8
        "wxyz", // 9
    };
public:
    vector<string> res;
    string tmp = "";
    vector<string> letterCombinations(string digits) {
        backtracking(digits, 0);
        return res;
    }

    void backtracking(string digits, int start) {
        if (tmp.size() == digits.size()) {
            res.push_back(tmp);
            return;
        }

        for (int i = start; i < digits.size(); i++) {
            string key = letterMap[digits[i] - '0'];
            for (int j = 0; j < key.size(); j++) {
                tmp += key[j];
                backtracking(digits, i + 1);
                tmp.resize(tmp.size() - 1);
            }
        }
    }
};
```