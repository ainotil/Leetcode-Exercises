# 代码随想录算法训练营 Day 11
150. 逆波兰表达式求值 | 239. 滑动窗口最大值 | 347. 前K个高频元素

---

## 150 - 逆波兰表达式求值
* 题目链接：[LeetCode 150 逆波兰表达式求值](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)
* 文章链接：[代码随想录讲解 逆波兰表达式求值](https://programmercarl.com/0150.%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%B1%82%E5%80%BC.html)

**看到题目的第一想法**  
挺简单的，理解逆波兰表达式，就会写了。

**看完代码随想录之后的想法**  
和我做的差不敌哦。

**实现过程中遇到的困难**   
无，一遍就写出来了。

---

### 代码
```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> s;
        for (int i = 0; i < tokens.size(); i++) {
            if (tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[i] == "/") { 
                int num = s.top();
                s.pop();
                if (tokens[i] == "+") {
                    num = s.top() + num;
                } else if (tokens[i] == "-") {
                    num = s.top() - num;
                } else if (tokens[i] == "*") {
                    num = s.top() * num;
                } else {
                    num = s.top() / num;
                }
                s.pop();
                s.push(num);
            } else {
                s.push(stoi(tokens[i]));
            }
        }
        return s.top();
    }
};
```

## 239 - 滑动窗口最大值
* 题目链接：[LeetCode 239 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)
* 文章链接：[代码随想录讲解 滑动窗口最大值](https://programmercarl.com/0239.%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%9C%80%E5%A4%A7%E5%80%BC.html)

**看到题目的第一想法**
我一开始在纠结使用栈还是队列，虽然没意识到应该使用双端队列，但是大体能想到`push`和`pop`所需要的条件。  
首先要排出所有在队列中的，已经不在滑动窗口的元素。这些元素都在队列的开始处，底部。  
其次还要排出所有在队列中的，比当前元素小的元素。现在队列中所有的元素都是滑动窗口内的，但我们不能只弹出队列底部的数字，而是要从顶部弹出。 
主要是要保证队列的最底部元素为最大值的索引。
到这里就不太会写了。

**看完代码随想录之后的想法**  
理解了双端队列，或者说单调队列的用法，更改数据结构后，就做对了。

**实现过程中遇到的困难**  
因为如果只是比对当前队列的底部数字，做弹出的话，按照这个逻辑，底部数字必然是当前窗口内最大的。然而队尾的元素才是还会在下次的窗口中的，所以为了保持队列从队首到队尾递减，我们要从队尾不断弹出这些小的元素。因为有我们当前的元素在的话，它们在之后窗口内永远不会成为最大值。
但是由于不知道双端队列，所以只差最后一步。

---

### 代码
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        deque<int> s;
        vector<int> res;

        for (int i = 0; i < nums.size(); i++) {

            if (!s.empty() && i - s.front() >= k) {
                s.pop_front();
            }

            while (!s.empty() && nums[i] >= nums[s.back()]) {
                s.pop_back();
            }

            s.push_back(i);

            if (i >= k - 1) {
                res.push_back(nums[s.front()]);
            }
        }

        return res;
    }
};
```

## 347 - 前K个高频元素
* 题目链接：[LeetCode 347 前K个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)
* 文章链接：[代码随想录讲解 前K个高频元素](https://programmercarl.com/0347.%E5%89%8DK%E4%B8%AA%E9%AB%98%E9%A2%91%E5%85%83%E7%B4%A0.html)

**看到题目的第一想法**
用哈希表再排序的解法，做出来了。

**看完代码随想录之后的想法** 
理解了大顶堆和小顶堆，理解后就好做了。   
首先，算频率，还需要排序的题用大顶堆和小顶堆都很合适。大顶堆以最高频率作为根节点，小顶堆以最小频率作为根节点。堆（heap）都是优先弹出根节点。这道题的主要思路是不断排出不需要的小频率节点，所以最终的堆会只有复合条件，`k`个最高频率节点。也就是说我们要用小顶堆，在收到 `> k` 个节点时开始弹出。

**实现过程中遇到的困难**  
主要是C++的语法。

---

### 代码
```cpp
class Solution {
public:

    class compare {
        public:
            bool operator()(const pair<int, int>& lhs, const pair<int, int>& rhs) {
                return lhs.second > rhs.second;
            }
    };

    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> map;
        for (int i = 0; i < nums.size(); i++) {
            map[nums[i]] += 1;
        }
        
        priority_queue<pair<int, int>, vector<pair<int, int>>, compare> q;

        for (const auto &p : map) {
            q.push(p);
            if (q.size() > k) {
                q.pop();
            }
        }

        vector<int> res(k);
        for (int i = k - 1; i >= 0; i--) {
            res[i] = q.top().first;
            q.pop();
        }

        return res;
    }
};
```

