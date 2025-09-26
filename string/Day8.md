# 代码随想录算法训练营 Day 8
344. 反转字符串 | 541. 反转字符串 II | 54. 替换数字

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

## 54 - 替换数字 II
* 题目链接：[卡码网 54 替换数字](https://kamacoder.com/problempage.php?pid=1064)
* 文章链接：[代码随想录讲解 替换数字](https://programmercarl.com/kamacoder/0054.%E6%9B%BF%E6%8D%A2%E6%95%B0%E5%AD%97.html#%E6%80%9D%E8%B7%AF)

**看到题目的第一想法**
还可以，这题不难。

**看完代码随想录之后的想法**  
看一眼基本上就知道怎么写了。

**实现过程中遇到的困难**  
如上。

---

### 代码
```cpp
#include <iostream>
using namespace std;
int main() {
    string s;
    while (cin >> s) {
        int old_size = s.size() - 1;
        int count = 0;
        for (int i = 0; i <= old_size; i++) {
            if (s[i] >= '0' and s[i] <= '9') {
                count += 1;
            }
        }
        s.resize(s.size() + count*5);
        int new_size = s.size() - 1;
        while(old_size >= 0) {
            if (s[old_size] >= '0' and s[old_size] <= '9') {
                s[new_size--] = 'r';
                s[new_size--] = 'e';
                s[new_size--] = 'b';
                s[new_size--] = 'm';
                s[new_size--] = 'u';
                s[new_size--] = 'n';
            } else {
                s[new_size--] = s[old_size];
            }
            old_size--;
        }
        cout << s << endl;       
    }
}

```