# 代码随想录算法训练营 Day 2
209. 长度最小的子数组

---

## 209 - 长度最小的子数组
* 题目链接：[LeetCode 209 长度最小的子数组](https://leetcode.cn/problems/minimum-size-subarray-sum/)
* 文章链接：[代码随想录讲解 长度最小的子数组](https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html)

**看到题目的第一想法**  
感觉自己会写，知道使用起始指针的终点指针的概念。但是细节有错，外加没有在主循环里加 `while` 循环，反而在主循环后又起了个循环，导致没做出来。

**看完代码随想录之后的想法**  
大概看了一眼和我写的差不多，但是在主循环里加 `while` 循环。

**实现过程中遇到的困难**  
跟着代码随想录，小改一番以后就对了。

---

### 代码
```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int res = 0;
        int sum = 0;
        int i = 0;
        for (int j = 0; j < nums.size(); j++) {
            sum += nums[j];
            while (sum >= target) {
                sum -= nums[i];
                res = (res < j - i + 1 && res != 0) ? res : j - i + 1;
                i++;
            }
        }
        return res;
    }
};
```

## 59 - 螺旋矩阵 II
* 题目链接：[LeetCode 59 螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/description/)
* 文章链接：[代码随想录讲解 螺旋矩阵 II](https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html)

**看到题目的第一想法**  
蒙了，没做过这种的。  

**看完代码随想录之后的想法**  
了解了这道题也是找区间，然后循环不变量，就好明白多了。

**实现过程中遇到的困难**  
有时会搞不明白先遍历 `i` 还是 `j` ，画图后更好理解。总之是先 `startX` 上升，`startY`上升，`startX` 下降，`startY` 下降。再使用 `offset` 和理解圈数等于 `n/2`。这题还是比较抽象的。

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n, 0));
        int startX = 0;
        int startY = 0;
        int offset = 1;
        int counter = 1;

        while (offset - 1 < n/2) {
            int i = startX;
            int j = startY;

            for (j = startY; j < n - offset; j++) {
                res[i][j] = counter++;
            }

            for (i = startX; i < n - offset; i++) {
                res[i][j] = counter++;
            }

            for(; j > startY; j--) {
                res[i][j] = counter++;
            }
            for(; i > startX; i--) {
                res[i][j] = counter++;
            }
            startY++;
            startX++;
            offset++;
        }
        if (n % 2) {
            res[n/2][n/2] = count;
        }
        return res;
    }
};
```
