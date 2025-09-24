# 代码随想录算法训练营 Day 8
344. 反转字符串 | 541. 反转字符串 II

---

## 344 - 反转字符串
* 题目链接：[LeetCode 344 反转字符串](https://leetcode.cn/problems/reverse-string/)
* 文章链接：[代码随想录讲解 反转字符串](https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

**看到题目的第一想法**  
挺简单的。

**看完代码随想录之后的想法**  
了解了C++库函数的使用。

**实现过程中遇到的困难**  
无

---

### 代码
```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        for (int i = 0, j = s.size() - 1; i < s.size() / 2; i++, j--) {
            swap(s[i], s[j]);
        }
    }
};
```

## 541 - 反转字符串 II
* 题目链接：[LeetCode 541 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii/)
* 文章链接：[代码随想录讲解 反转字符串 II](https://programmercarl.com/0541.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2II.html)

**看到题目的第一想法**
知道怎么做，但是细节有错，做不出来。  

**看完代码随想录之后的想法**  
感觉这道题的循环条件比较复杂，得搞明白这点。

**实现过程中遇到的困难**  
如上。

---

### 代码
```cpp
class Solution {
public:
    void reverse(string& s, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            swap(s[i], s[j]);
        }
    }

    string reverseStr(string s, int k) {
        for (int i = 0; i < s.size(); i+=2*k) {
            if (i + k <= s.size()) {
                reverse(s, i, i + k - 1);
                continue;
            }
            reverse(s, i, s.size() - 1);
        }
        return s;
    }
};
```