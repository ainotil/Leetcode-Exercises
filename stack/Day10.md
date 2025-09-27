# 代码随想录算法训练营 Day 10
232. 用栈实现队列 | 225. 用队列实现栈 | 20. 有效的括号 | 1047. 删除字符串中的所有相邻重复项

---

## 232 - 用栈实现队列
* 题目链接：[LeetCode 232 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/)
* 文章链接：[代码随想录讲解 用栈实现队列](https://programmercarl.com/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.html)

**看到题目的第一想法**  
理解这道题怎么做，但是C++的语法不太熟悉。

**看完代码随想录之后的想法**  
还可以，掌握了栈在C++里的语法。

**实现过程中遇到的困难**  
无。
---

### 代码
```cpp
class MyQueue {
public:

    // stack: first in last out
    // queue: first in first out
    stack<int> stIn;
    stack<int> stOut;

    MyQueue() {
        
    }
    
    void push(int x) {
        stIn.push(x);
    }
    
    int pop() {
        if (stOut.empty()) {
            while(!stIn.empty()) {
                stOut.push(stIn.front());
                stIn.pop();
            }
        }
        int result = stOut.front();
        stOut.pop();
        return result;
    }
    
    int peek() {
        int res = this->pop();
        stOut.push(res);
        return res;
    }
    
    bool empty() {
        return stOut.empty() && stIn.empty();
    }
};
```

## 225 - 用队列实现栈
* 题目链接：[LeetCode 225 用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues/)
* 文章链接：[代码随想录讲解 用队列实现栈](https://programmercarl.com/0225.%E7%94%A8%E9%98%9F%E5%88%97%E5%AE%9E%E7%8E%B0%E6%A0%88.html)

**看到题目的第一想法**  
不太会做。

**看完代码随想录之后的想法**  
这道题比上一题难，用一个队列的诀窍就是不断pop和push同时来。

**实现过程中遇到的困难**  
无。

---

### 代码
```cpp
class MyStack {
public:

    queue<int> q;

    MyStack() {
        
    }
    
    void push(int x) {
        q.push(x);
    }
    
    int pop() {
        int size = q.size() - 1;
        while(size > 0) {
            q.push(q.front());
            q.pop();
            size--;
        } 
        int res = q.front();
        q.pop();
        return res;
    }
    
    int top() {
        int size = q.size() - 1;
        while(size > 0) {
            q.push(q.front());
            q.pop();
            size--;
        } 
        int res = q.front();
        q.push(q.front());  
        q.pop();
        return res;
    }
    
    bool empty() {
        return q.empty();
    }
};
```

## 20 - 有效的括号
* 题目链接：[LeetCode 20 有效的括号](https://leetcode.cn/problems/valid-parentheses/)
* 文章链接：[代码随想录讲解 有效的括号](https://programmercarl.com/0020.%E6%9C%89%E6%95%88%E7%9A%84%E6%8B%AC%E5%8F%B7.html)

**看到题目的第一想法**  
这题做过，不难。做一遍对了。

**看完代码随想录之后的想法**  
我觉得我的做法比较符合我的理解。代码随想录的解法的代码量少一些，但是内存和运行时间没区别。

**实现过程中遇到的困难**  
无。
---

### 代码
```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<int> tmp;
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(' || s[i] == '{' || s[i] == '[') {
                tmp.push(s[i]);
            } else {
                if (tmp.empty()) {
                    return false;
                }
                if (s[i] == ')' && tmp.top() != '(') {
                    return false;
                } else if (s[i] == '}' && tmp.top() != '{') {
                    return false;
                } else if (s[i] == ']' && tmp.top() != '[') {
                    return false;
                } else {
                    tmp.pop();
                }
            }
        }
        return tmp.empty();
    }
};
```

## 1047 - 删除字符串中的所有相邻重复项
* 题目链接：[LeetCode 1047 删除字符串中的所有相邻重复项](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)
* 文章链接：[代码随想录讲解 删除字符串中的所有相邻重复项](https://programmercarl.com/1047.%E5%88%A0%E9%99%A4%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E6%89%80%E6%9C%89%E7%9B%B8%E9%82%BB%E9%87%8D%E5%A4%8D%E9%A1%B9.html)

**看到题目的第一想法**  
做一遍就对了。

**看完代码随想录之后的想法**  
主要是了解了字符串怎么当作栈使用。

**实现过程中遇到的困难**  
C++语法。
---

### 代码
```cpp
class Solution {
public:
    string removeDuplicates(string S) {
        string res;
        for (char s : S) {
            if (res.empty() || res.back() != s) {
                res.push_back(s);
            } else {
                res.pop_back();
            }
        }
        return res;
    }
};
```