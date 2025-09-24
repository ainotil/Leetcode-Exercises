# 代码随想录算法训练营 Day 6
242. 有效的字母异位词 | 349. 两个数组的交集 | 202. 快乐数 | 1. 两数之和
---
## 242 - 有效的字母异位词
* 题目链接：[LeetCode 242 有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)
* 文章链接：[代码随想录讲解 有效的字母异位词](https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html)

**看到题目的第一想法**
知道使用哈希表，比较简单。

**看完代码随想录之后的想法**  
和我的解法一样。

**实现过程中遇到的困难**  
无。

---

### 代码
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) {
            return false;
        }
        vector<int> ascii(26, 0);
        for (int i = 0; i < s.length(); i++) {
            ascii[s[i] - 97] += 1;
        }

        for (int i = 0; i < t.length(); i++) {
            ascii[t[i] - 97] -= 1;
        }

        for (int i = 0; i < 26; i++) {
            if (ascii[i] != 0) {
                return false;
            }
        }
        return true;
    }
};
```

## 349 - 两个数组的交集
* 题目链接：[LeetCode 349 两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/)
* 文章链接：[代码随想录讲解 两个数组的交集](https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html)

**看到题目的第一想法**  
对于C++其实我不熟，不太知道 `set` 的用法。我知道 `set` 的特性，但不太知道怎么使用。

**看完代码随想录之后的想法**  
主要是看语法，和C++里不同数据结构的底层逻辑。  
`set`  和 `multiset` 底层实现都是红黑树，`unordered_set` 的底层实现是哈希表， 使用 `unordered_set` 读写效率是最高的。  
此题并不需要对数据进行排序，而且还不要让数据重复，所以选择 `unordered_set`。

**实现过程中遇到的困难**  
没太理解 `s.find(nums2[i]) != s.end()`。`set.find()` 函数会一个个找元素，找不到的时候就会指向尾后迭代器 `set.end()`。尾后迭代器不代表任何元素，只是一个虚拟的位置，指向最后一个元素之后的位置，`set` 和 `map` 也支持尾后迭代器。

---

### 代码
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> res;
        unordered_set<int> s(nums1.begin(), nums1.end());
        for (int i = 0; i < nums2.size(); i++) {
            if (s.find(nums2[i]) != s.end()) {
                res.insert(nums2[i]);
            }
        }
        return vector<int>(res.begin(), res.end());
    }
};
```

## 202 - 快乐数
* 题目链接：[LeetCode 202 快乐数](https://leetcode.cn/problems/happy-number/)
* 文章链接：[代码随想录讲解 快乐数](https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html)

**看到题目的第一想法**  
和上一题差不多，做出来了。但是执行用时和消耗内存都不是很理想。

**看完代码随想录之后的想法**  
无。

**实现过程中遇到的困难**  
找和有点麻烦，不过还好。

---

### 代码
```cpp
class Solution {
public:
    bool isHappy(int n) {
        unordered_set<int> sums;
        sums.insert(-1);
        while (true) {
            int tmp = 0;
            while (n > 0) {
                tmp += (n % 10) * (n % 10);
                n /= 10;
            }
            n = tmp;
            if (tmp == 1) {
                return true;
            } else if (sums.find(tmp) != sums.end()) {
                return false;
            } else {
                sums.insert(tmp);
            }
        }
        return true;
    }
};
```

## 1 - 两数之和
* 题目链接：[LeetCode 1 两数之和](https://leetcode.cn/problems/two-sum/)
* 文章链接：[代码随想录讲解 两数之和](https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html)

**看到题目的第一想法**  
知道怎么写。

**看完代码随想录之后的想法**  
无。

**实现过程中遇到的困难**   
C++的语法不太熟。

---
### 代码
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map <int,int> map;
        for (int i = 0; i < nums.size(); i++) {
            auto iter = map.find(target - nums[i]); 
            if(iter != map.end()) {
                return {iter->second, i};
            }
            map.insert(pair<int, int>(nums[i], i));
        }
        return {};
    }
};
```