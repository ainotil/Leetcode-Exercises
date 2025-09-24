# 代码随想录算法训练营 Day 7
454. 四数相加 II | 383. 救赎金 | 15. 三数之和 | 18. 四数之和
---
## 454 - 四数相加 II
* 题目链接：[LeetCode 454 四数相加 II](https://leetcode.cn/problems/4sum-ii/)
* 文章链接：[代码随想录讲解 四数相加 II](https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html)

**看到题目的第一想法**  
有点儿懵，不知道怎么写。

**看完代码随想录之后的想法**  
其实就是两个两数之和。

**实现过程中遇到的困难**  
C++语法的问题。

---

### 代码
```cpp
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map <int,int> map;
        for (int i = 0; i < nums1.size(); i++) {
            for (int j = 0; j < nums2.size(); j++) {
                map[nums1[i] + nums2[j]] += 1;
            }
        }

        int res = 0;
        for (int i = 0; i < nums3.size(); i++) {
            for (int j = 0; j < nums4.size(); j++) {
                if (map.find(-nums3[i]-nums4[j]) != map.end()) {
                    res += map[-nums3[i]-nums4[j]];
                }
            }
        }
        return res;
    }
};
```

## 383 - 救赎金
* 题目链接：[LeetCode 383 救赎金](https://leetcode.cn/problems/ransom-note/)
* 文章链接：[代码随想录讲解 救赎金](https://programmercarl.com/0383.%E8%B5%8E%E9%87%91%E4%BF%A1.html)

**看到题目的第一想法**  
比较简单。

**看完代码随想录之后的想法**  
无。

**实现过程中遇到的困难**  
无。

---

### 代码
```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        vector<int> ascii(26, 0);

        for (int i = 0; i < magazine.size(); i++) {
            ascii[magazine[i] - 'a'] += 1;
        }

        for (int i = 0; i < ransomNote.size(); i++) {
            ascii[ransomNote[i] - 'a'] -= 1;
            if (ascii[ransomNote[i] - 'a'] < 0) {
                return false;
            }
        }
        return true;
    }
};
```

## 15 - 三数之和
* 题目链接：[LeetCode 15 三数之和](https://leetcode.cn/problems/3sum/)
* 文章链接：[代码随想录讲解 三数之和](https://programmercarl.com/0015.%E4%B8%89%E6%95%B0%E4%B9%8B%E5%92%8C.html)

**看到题目的第一想法**  
知道怎么用哈希表完成，但不会双指针解法。

**看完代码随想录之后的想法**  
这题还是挺难的，主要是在去重的地方怎么利用数组已经被排序的特性。

**实现过程中遇到的困难**  
首先，先意识到使用双指针。  
其次，因为数组已经被排序了。这题能有重复的元素，但是最终的结果中不能有重复的三元组。所以当数组已经被排序的时候，双指针解法只会从当前元素后的数组选出两个元素。如果当前相同元素已经被遍历过了，说明接下来找的两个元素会是重复的三元组。  
同理，在做双指针解法的时候，既然两个指针是一起向内合并的，所以我们每次有解的时候，也要利用排序后相同元素相邻的特性。排除相同元素。

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > 0) {
                return res;
            }
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int left = i + 1;
            int right = nums.size() - 1;
            while (left < right) {
                if (nums[i] + nums[left] + nums[right] > 0) {
                    right -= 1;
                } else if (nums[i] + nums[left] + nums[right] < 0) {
                    left += 1;
                } else {
                    res.push_back({nums[i], nums[left], nums[right]});
                    while (right > left && nums[right] == nums[right - 1]) right--;
                    while (right > left && nums[left] == nums[left + 1]) left++;

                    right--;
                    left++;
                }
            }
        }
        return res;
    }
};
```

## 18 - 四数之和
* 题目链接：[LeetCode 18 四数之和](https://leetcode.cn/problems/4sum/)
* 文章链接：[代码随想录讲解 四数之和](https://programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html)

**看到题目的第一想法**  
和三数之和很像。

**看完代码随想录之后的想法**  
确实就是三数之和的延申版。

**实现过程中遇到的困难**  
这道题相比较三数之和，多了两个难点。  
首先是更多的剪枝。我们要考虑到 `target` 可能是负数，所以不能只考虑到当前的和是大于 `target` 的时候剪枝，还得保证当前和是正数。不然当前和仍然可能与更大的负数或某些负数+正数组成和为 `target` 的组合。  
其次是一层套一层的循环的安排。需要多注意不要遍历已经遍历过的元素。

---

### 代码
```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] > target && nums[i] >= 0) {
                return res;
            }
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[i] + nums[j] > target && nums[j] + nums[i] >= 0) {
                    break;
                }
                if (j > i + 1 && nums[j] == nums[j - 1]) {
                    continue;
                }
                int left = j + 1;
                int right = nums.size() - 1;
                while (left < right) {
                    if ((long)nums[i] + nums[j] + nums[left] + nums[right] > target) {
                        right -= 1;
                    } else if ((long)nums[i]  + nums[j] + nums[left] + nums[right] < target) {
                        left += 1;
                    } else {
                        res.push_back({nums[i], nums[j], nums[left], nums[right]});
                        while (right > left && nums[right] == nums[right - 1]) right--;
                        while (right > left && nums[left] == nums[left + 1]) left++;

                        right--;
                        left++;
                    }
                }
            }
        }
        return res;
    }
};
```