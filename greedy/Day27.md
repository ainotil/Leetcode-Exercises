# 代码随想录算法训练营 Day 27   
452. 用最少数量的箭引爆气球 | 435. 无重叠区间 | 763. 划分字母区间

---

## 452. 用最少数量的箭引爆气球
* 题目链接：[LeetCode 452. 用最少数量的箭引爆气球](https://leetcode.cn/problems/minimum-number-of-arrows-to-burst-balloons/)
* 文章链接：[代码随想录讲解 用最少数量的箭引爆气球](https://programmercarl.com/0452.%E7%94%A8%E6%9C%80%E5%B0%91%E6%95%B0%E9%87%8F%E7%9A%84%E7%AE%AD%E5%BC%95%E7%88%86%E6%B0%94%E7%90%83.html)

**看到题目的第一想法**    
秒了，但是代码表现不好。   

**看完代码随想录之后的想法**    
优化后好了一些，没有创建另一个变量就好了。   

**实现过程中遇到的困难**  
无。   
   
---

### 代码
```cpp
class Solution {
public:
    static bool cmp(vector<int> a, vector<int> b) {
        return a[0] < b[0];
    }
    int findMinArrowShots(vector<vector<int>>& points) {
        sort(points.begin(), points.end(), cmp);

        int res = 1;
        for (int i = 1; i < points.size(); i++) {
            if (points[i][0] > points[i - 1][1]) {
                res += 1;
            } else {
                points[i][1] = min(points[i - 1][1], points[i][1]);
            }
        }

        return res;
    }
};
```

## 435. 无重叠区间
* 题目链接：[LeetCode 435. 无重叠区间](https://leetcode.cn/problems/non-overlapping-intervals/)
* 文章链接：[代码随想录讲解 无重叠区间](https://programmercarl.com/0435.%E6%97%A0%E9%87%8D%E5%8F%A0%E5%8C%BA%E9%97%B4.html)

**看到题目的第一想法**     
有思路，但是做不对。       
 
**看完代码随想录之后的想法**    
思路更清晰了，原本的方向是对的。主要就是考虑重合的时候，判定重合，更新边界。     

**实现过程中遇到的困难**  
无。   
   
---

### 代码
```cpp
class Solution {
public:
    static bool cmp(vector<int> a, vector<int>b) {
        return a[0] < b[0];
    }
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), cmp);

        int res = 0;

        for (int i = 1; i < intervals.size(); i++) {
            if (intervals[i - 1][1] > intervals[i][0]) {
                intervals[i][1] = min(intervals[i - 1][1], intervals[i][1]);
                res += 1;
            }
        }

        return res;
    }
};
```

## 763. 划分字母区间
* 题目链接：[LeetCode 763. 划分字母区间](https://leetcode.cn/problems/partition-labels/)
* 文章链接：[代码随想录讲解 划分字母区间](https://programmercarl.com/0763.%E5%88%92%E5%88%86%E5%AD%97%E6%AF%8D%E5%8C%BA%E9%97%B4.html)

**看到题目的第一想法**     
没想到可以使用哈希表。       
 
**看完代码随想录之后的想法**    
思路更清晰了，这道题不难，使用哈希表来得到最远距离。        

**实现过程中遇到的困难**  
无。   
   
---

### 代码
```cpp
class Solution {
public:
    vector<int> partitionLabels(string S) {
        int hash[27] = {0}; // i为字符，hash[i]为字符出现的最后位置
        for (int i = 0; i < S.size(); i++) { // 统计每一个字符最后出现的位置
            hash[S[i] - 'a'] = i;
        }
        vector<int> result;
        int left = 0;
        int right = 0;
        for (int i = 0; i < S.size(); i++) {
            right = max(right, hash[S[i] - 'a']); // 找到字符出现的最远边界
            if (i == right) {
                result.push_back(right - left + 1);
                left = i + 1;
            }
        }
        return result;
    }
};
```
