# 代码随想录算法训练营 Day 1
704. 二分查找 | 27. 移除元素 | 977. 有序数组的平方

---

## 704 - 二分查找
* 题目链接：[LeetCode 704 二分查找](https://leetcode.cn/problems/binary-search/)
* 文章链接：[代码随想录讲解 二分查找](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html)

**看到题目的第一想法**  
非常经典，用 `left` 和 `right` 两个指针一次次进行一分为二的分割。  
不是很难，但不一定能一次写出来。

**看完代码随想录之后的想法**  
理解了左闭右闭和左闭右开的概念，以及在解题中的重要性。

**实现过程中遇到的困难**  
有时会搞混怎么设置 `left` 和 `right`。  
当 `nums[middle]` 大于 `target` 时，说明 `target` 在 `nums[middle]` 的左边，  
如果想要搜索范围缩到左边，就需要更新 `right = middle - 1` （左闭右闭）。

---

### 代码
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;

        while (left <= right) {
            int middle = (left + right) / 2;
            if (nums[middle] > target) {
                right = middle - 1;
            } else if (nums[middle] < target) {
                left = middle + 1;
            } else {
                return middle;
            }
        }

        return -1;
    }
};
```

## 27 - 移除元素 
* 题目链接：[LeetCode 27 移除元素](https://leetcode.cn/problems/remove-element/)
* 文章链接：[代码随想录讲解 移除元素](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html)

**看到题目的第一想法**  
应该之前做过这道题，记得是使用双指针的做法。但思路并不清晰。

**看完代码随想录之后的想法**  
快指针是用来获取新数组中该有（除去 `val`）的元素，慢指针是获取我们新数组中需要更新的位置。

**实现过程中遇到的困难**  
有时会搞混更新数组的时机，我们应该用 `nums[fast] != val`，代表只有不是 `val` 的元素才能被加入新数组，从而也更新慢指针。

---

### 代码
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow = 0;
        int fast = 0;
        for (fast = 0; fast < nums.size(); fast++) {
            if (nums[fast] != val) {
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;
    }
};
```

## 27 - 移除元素 
* 题目链接：[LeetCode 27 移除元素](https://leetcode.cn/problems/remove-element/)
* 文章链接：[代码随想录讲解 移除元素](https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html)

**看到题目的第一想法**  
应该之前做过这道题，记得是使用双指针的做法。但思路并不清晰。

**看完代码随想录之后的想法**  
快指针是用来获取新数组中该有（除去 `val`）的元素，慢指针是获取我们新数组中需要更新的位置。

**实现过程中遇到的困难**  
有时会搞混更新数组的时机，我们应该用 `nums[fast] != val`，代表只有不是 `val` 的元素才能被加入新数组，从而也更新慢指针。

---

### 代码
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int slow = 0;
        int fast = 0;
        for (fast = 0; fast < nums.size(); fast++) {
            if (nums[fast] != val) {
                nums[slow] = nums[fast];
                slow++;
            }
        }
        return slow;
    }
};
```

## 977 - 有序数组的平方 
* 题目链接：[LeetCode 977 有序数组的平方](https://leetcode.cn/problems/squares-of-a-sorted-array/)
* 文章链接：[代码随想录讲解 有序数组的平方](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html
)

**看到题目的第一想法**  
这题很简单，利用最小正数的平方是最小的特点，找出第一个 `>= 0` 的元素，再使用双指针，一个向左搜索一个向右优先搜索最小绝对值，即可获取答案。就是有点儿繁琐。

**看完代码随想录之后的想法**  
我意识到我的答案有内存用了太多的缺点，代码随想录的答案先更加巧妙。先用dummy variables填满要返回的数组，再优先加入最大的元素。

**实现过程中遇到的困难**  
暂时没有，这算我之前做过的题并且还记住怎么做的题。

---

### 代码
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        vector<int> res(nums.size(), 0);
        int k = nums.size() - 1;
        for (int i = 0, j = nums.size() - 1; i <= j;) {
            if (nums[i] * nums[i] > nums[j] * nums[j]) {
                res[k--] = nums[i]*nums[i];
                i++;
            } else {
                res[k--] = nums[j]*nums[j];
                j--;
            }
        }
        return res;
    }
};
```