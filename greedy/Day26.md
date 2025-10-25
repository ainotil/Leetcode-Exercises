# 代码随想录算法训练营 Day 26   
134. 加油站 | 135. 分发糖果 | 860. 柠檬水找零

---

## 134. 加油站
* 题目链接：[LeetCode 134. 加油站](https://leetcode.cn/problems/gas-station/)
* 文章链接：[代码随想录讲解 加油站](https://programmercarl.com/0134.%E5%8A%A0%E6%B2%B9%E7%AB%99.html)

**看到题目的第一想法**    
观察出来应该使用`gas[i] - cost[i]`这个差值，也知道当差值小于`0`时应该做什么，但不太确定需要做什么。

**看完代码随想录之后的想法**    
明白了当`currSum < 0`时，这个区段就不能走，会断油，所以要考虑之后的可能。

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int currSum = 0;
        int totalSum = 0;
        int res = 0;

        for (int i = 0; i < gas.size(); i++) {
            totalSum += gas[i] - cost[i];
            currSum += gas[i] - cost[i];
            if (currSum < 0) {
                currSum = 0;
                res = i + 1;
            }
        }

        if (totalSum < 0) {
            return -1;
        } else {
            return res;
        }
    }
};
```

## 135. 分发糖果
* 题目链接：[LeetCode 135. 分发糖果](https://leetcode.cn/problems/candy/)
* 文章链接：[代码随想录讲解 分发糖果](https://programmercarl.com/0135.%E5%88%86%E5%8F%91%E7%B3%96%E6%9E%9C.html)

**看到题目的第一想法**    
不太会写。

**看完代码随想录之后的想法**    
主要是要检查左右相邻再增加值，左遍历一次右遍历一次，两次检查，就能保证正确了。   

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int currSum = 0;
        int totalSum = 0;
        int res = 0;

        for (int i = 0; i < gas.size(); i++) {
            totalSum += gas[i] - cost[i];
            currSum += gas[i] - cost[i];
            if (currSum < 0) {
                currSum = 0;
                res = i + 1;
            }
        }

        if (totalSum < 0) {
            return -1;
        } else {
            return res;
        }
    }
};
```

## 860. 柠檬水找零
* 题目链接：[LeetCode 860. 柠檬水找零](https://leetcode.cn/problems/lemonade-change/)
* 文章链接：[代码随想录讲解 柠檬水找零](https://programmercarl.com/0860.%E6%9F%A0%E6%AA%AC%E6%B0%B4%E6%89%BE%E9%9B%B6.html)

**看到题目的第一想法**    
简单。   

**看完代码随想录之后的想法**    
无。   

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int currSum = 0;
        int totalSum = 0;
        int res = 0;

        for (int i = 0; i < gas.size(); i++) {
            totalSum += gas[i] - cost[i];
            currSum += gas[i] - cost[i];
            if (currSum < 0) {
                currSum = 0;
                res = i + 1;
            }
        }

        if (totalSum < 0) {
            return -1;
        } else {
            return res;
        }
    }
};
```

## 406. 根据身高重建队列
* 题目链接：[LeetCode 406. 根据身高重建队列](https://leetcode.cn/problems/queue-reconstruction-by-height)
* 文章链接：[代码随想录讲解 根据身高重建队列](https://programmercarl.com/0406.%E6%A0%B9%E6%8D%AE%E8%BA%AB%E9%AB%98%E9%87%8D%E5%BB%BA%E9%98%9F%E5%88%97.html)

**看到题目的第一想法**    
这题难，没想法。   

**看完代码随想录之后的想法**    
厉害厉害，先按照h排序，就决定了基本的顺序。再按照k进行插入，就能保证插入的位置前的元素都是大于或者等于当前元素的。   

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    static bool cmp(vector<int>&a ,vector<int>& b) {
        if (a[0] == b[0]) {
            return a[1] < b[1];
        }
        return a[0] > b[0];
    }

    vector<vector<int>> reconstructQueue(vector<vector<int>>& people) {
        sort(people.begin(), people.end(), cmp);
        vector<vector<int>> res;
        for (int i = 0; i < people.size(); i++) {
            res.insert(res.begin() + people[i][1], people[i]);
        }
        return res;
    }
};
```