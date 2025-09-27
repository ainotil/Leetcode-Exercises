# 代码随想录算法训练营 Day 9
151. 翻转字符串里的单词 | 55. 右旋转字符串

---

## 151 - 翻转字符串里的单词
* 题目链接：[LeetCode 151 翻转字符串里的单词](https://leetcode.cn/problems/reverse-words-in-a-string/)
* 文章链接：[代码随想录讲解 翻转字符串里的单词](https://programmercarl.com/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.html)

**看到题目的第一想法**  
一知半解。

**看完代码随想录之后的想法**  
主要是要分成三步，先移除多余的空格，再反转整个字符串来调转单词位置，再把每个单词反转会来。意识到这三步就简单了。

**实现过程中遇到的困难**  
有点难，但是也可以自己写出来。
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

## 55 - 右旋转字符串
* 题目链接：[卡码网 55 右旋转字符串](https://kamacoder.com/problempage.php?pid=1065)
* 文章链接：[代码随想录讲解 右旋转字符串](https://programmercarl.com/kamacoder/0055.%E5%8F%B3%E6%97%8B%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

**看到题目的第一想法**  
不会写，没什么想法。

**看完代码随想录之后的想法**  
主要是要分成三步，先反转整个字符串，再反转两个小字符串。意识到这两步就简单了。

**实现过程中遇到的困难**  
没困难。

---

### 代码
```cpp
#include<iostream>
#include<algorithm>
using namespace std;
int main() {
    int n;
    string s;
    cin >> n;
    cin >> s;
    reverse(s.begin(), s.end());
    reverse(s.begin(), s.begin() + n);
    reverse(s.begin() + n, s.end());
    cout << s << endl;
}
```
