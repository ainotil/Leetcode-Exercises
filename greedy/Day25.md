# 代码随想录算法训练营 Day 25   
122. 买卖股票的最佳时机II | 55. 跳跃游戏 | 45. 跳跃游戏II | 1005. K次取反后最大化的数组和

---

## 122. 买卖股票的最佳时机II
* 题目链接：[LeetCode 122. 买卖股票的最佳时机II](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/)
* 文章链接：[代码随想录讲解 买卖股票的最佳时机II](https://programmercarl.com/0122.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAII.html)

**看到题目的第一想法**    
能写，秒了。主要是得观察规律。  

**看完代码随想录之后的想法**    
无。

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int res = 0;

        for (int i = 1; i < prices.size(); i++) {
            if (prices[i] - prices[i-1] >= 0) {
                res += prices[i] - prices[i-1];
            }
        }

        return res;
    }
};
```

## 55. 跳跃游戏
* 题目链接：[LeetCode 55. 跳跃游戏](https://leetcode.cn/problems/jump-game)
* 文章链接：[代码随想录讲解 跳跃游戏](https://programmercarl.com/0055.%E8%B7%B3%E8%B7%83%E6%B8%B8%E6%88%8F.html)

**看到题目的第一想法**    
想到覆盖范围了，但是细节不对，比如循环的条件，什么时候结束循环。    

**看完代码随想录之后的想法**    
对于覆盖范围的理解更多了。    

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        if (nums.size() == 1) {
            return true;
        }

        int res = 0;
        for (int i = 0; i <= res; i++) {
            res = max(i + nums[i], res);
            if (res >= nums.size() - 1) {
                return true;
            }
        }
        return false;
    }
};
```

## 45. 跳跃游戏II 
* 题目链接：[LeetCode 45. 跳跃游戏II](https://leetcode.cn/problems/jump-game-ii/)
* 文章链接：[代码随想录讲解 跳跃游戏II](https://programmercarl.com/0045.%E8%B7%B3%E8%B7%83%E6%B8%B8%E6%88%8FII.html)

**看到题目的第一想法**    
细节写不对。    

**看完代码随想录之后的想法**    
主要是没写对`nums.size() - 1`。感觉贪婪算法还是挺难看出来的，只能多刷题。  

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        if (nums.size() == 1) {
            return 0;
        }

        int step = 0;
        int currFarthest = 0;
        int currEnd = 0;

        for (int i = 0; i < nums.size() - 1; i++) {
            currFarthest = max(currFarthest, i + nums[i]);
            if (i == currEnd) {
                step += 1;
                currEnd = currFarthest;
            }
        }
        return step;
    }
};
```

## 1005. K次取反后最大化的数组和
* 题目链接：[LeetCode 1005. K次取反后最大化的数组和](https://leetcode.cn/problems/maximize-sum-of-array-after-k-negations/)
* 文章链接：[代码随想录讲解 K次取反后最大化的数组和](https://programmercarl.com/0045.%E8%B7%B3%E8%B7%83%E6%B8%B8%E6%88%8FII.html)

**看到题目的第一想法**    
花了一些时间写出来的，有点长。  

**看完代码随想录之后的想法**    
主要是得写出靠绝对值排序，我觉得我的写法更好理解。

**实现过程中遇到的困难**  
无。
   
---

### 代码
```cpp
class Solution {
public:
    int largestSumAfterKNegations(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end());
        
        for (int i = 0; i < nums.size() && k > 0; i++) {
            if (nums[i] < 0) {
                nums[i] = -nums[i];
                k--;
            }
        }

        if (k % 2 == 1) {
            sort(nums.begin(), nums.end());
            nums[0] = -nums[0];
        }

        int res = 0;
        for (int i = 0; i < nums.size(); i++) {
            res += nums[i];
        }
        return res;
    }
};
```