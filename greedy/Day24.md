# 代码随想录算法训练营 Day 24   
455. 分发饼干 | 376. 摆动序列 | 53. 最大子序和

---

## 455. 分发饼干
* 题目链接：[LeetCode 455. 分发饼干](https://leetcode.cn/problems/assign-cookies)
* 文章链接：[代码随想录讲解 分发饼干](https://programmercarl.com/0455.%E5%88%86%E5%8F%91%E9%A5%BC%E5%B9%B2.html)

**看到题目的第一想法**    
能写，秒了。

**看完代码随想录之后的想法**    
比我写的简洁，但是我觉得我的更好理解。      

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int res = 0;
        int i = 0;
        int j = 0;
        while (i < g.size() && j < s.size()) {
            if (g[i] <= s[j]) {
                res += 1;
                i += 1;
                j += 1;
            } else {
                j += 1;
            }
        }
        return res;
    }
};
```

## 376. 摆动序列
* 题目链接：[LeetCode 376. 摆动序列](https://leetcode.cn/problems/wiggle-subsequence/)
* 文章链接：[代码随想录讲解 摆动序列](https://programmercarl.com/0376.%E6%91%86%E5%8A%A8%E5%BA%8F%E5%88%97.html)

**看到题目的第一想法**    
写不太对，主要是平坡的处理。

**看完代码随想录之后的想法**    
代码随想录的解法有两点，一是去掉相同的元素，可以通过`prevDiff == 0`这部分来排除平坡。二是更新`prevDiff`的时候，因为我们需要排除掉连续的上升和下降，所以只有在符合条件时才记录`prevDiff`。        

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        if (nums.size() < 2) {
            return nums.size();
        }
        int res = 1;
        int prevDiff = 0;
        int currDiff = 0;
        for (int i = 0; i < nums.size() - 1; i++) {
            currDiff = nums[i + 1] - nums[i];
            if ((prevDiff <= 0 && currDiff > 0) || (prevDiff >= 0 && currDiff < 0)) {
                res += 1;
                prevDiff = currDiff;
            }
            
        }
        return res;
    }
};
```

## 53. 最大子序和
* 题目链接：[LeetCode 53. 最大子序和](https://leetcode.cn/problems/maximum-subarray/)
* 文章链接：[代码随想录讲解 最大子序和](https://programmercarl.com/0053.%E6%9C%80%E5%A4%A7%E5%AD%90%E5%BA%8F%E5%92%8C.html)

**看到题目的第一想法**    
这道题不太难。

**看完代码随想录之后的想法**    
无。        

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res = INT32_MIN;
        int sum = 0;
        for (int i = 0; i < nums.size(); i++) {
            sum += nums[i];
            res = max(res, sum);
            if (sum <= 0) {
                sum = 0;
            }
        }
        return res;
    }
};
```