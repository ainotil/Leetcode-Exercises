# 代码随想录算法训练营 Day 3
203. 移除链表元素 | 707.设计链表 | 206.反转链表

---

## 203 - 移除链表元素
* 题目链接：[LeetCode 203 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)
* 文章链接：[代码随想录讲解 移除链表元素](https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html)

**看到题目的第一想法**  
大一刚开始学C时老师教过，当时链表学的比数组好，所以还有印象。记得分成头和中两种情况解决，一遍就做出来了。

**看完代码随想录之后的想法**  
代码随想录提供了两种解法，一种遍历，一种递归。  
我写的版本是遍历，写的比较随意，不够简洁。看完代码随想录后，先是想起来 `curr->next = curr->next->next`，就发现自己的代码不够简介了。了解了虚拟头节点的概念，其实和我使用的的 `previous` 差不多，但是更好。

**实现过程中遇到的困难**  
还好，这题不难。

---

### 代码
```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* curr = dummy;
        while (curr->next != nullptr) {
            if (curr->next->val == val) {
                curr->next = curr->next->next;
            } else {
                curr = curr->next;
            }
            
        }
        return dummy->next;
    }
};
```

## 707 - 设计链表
* 题目链接：[LeetCode 707 设计链表](https://leetcode.cn/problems/design-linked-list)
* 文章链接：[代码随想录讲解 设计链表](https://programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html
)

**看到题目的第一想法**  
比较简单，做了一会儿做出来了。但是实际用时和内存都不是很理想。

**看完代码随想录之后的想法**  
用虚拟头节点和 `size` 后，用时和内存都得到了提升。

**实现过程中遇到的困难**  
还好，这题不难。

---

### 代码
```cpp
class MyLinkedList {

public:
    struct Node {
        int val;
        Node* next;
        Node(int val) : val(val), next(nullptr) {}
    };

    MyLinkedList() {
        dummy = new Node(0);
        size = 0;
    }
    
    int get(int index) {
        if (index < 0 || index > size - 1) {
            return -1;
        }
        Node* curr = dummy->next;
        while(index--) {
            curr = curr->next;
        }
        return curr->val;
    }
    
    void addAtHead(int val) {
        Node* new_node = new Node(val);
        new_node->next = dummy->next;
        dummy->next = new_node;
        size++;
    }
    
    void addAtTail(int val) {
        Node* new_node = new Node(val);
        Node* curr = dummy;
        while(curr->next != nullptr) {
            curr = curr->next;
        }
        curr->next = new_node;
        size++;
    }
    
    void addAtIndex(int index, int val) {
        if (index < 0 || index > size) {
            return;
        }
        Node*curr = dummy;
        while(index--) {
            curr = curr->next;
        }
        Node* new_node = new Node(val);
        new_node->next = curr->next;
        curr->next = new_node;
        size++;
    }
    
    void deleteAtIndex(int index) {
        if (index < 0 || index > size - 1) {
            return;
        }
        Node*curr = dummy;
        while(index--) {
            curr = curr->next;
        }
        Node* tmp = curr->next;
        curr->next = curr->next->next;
        delete tmp;
        tmp = nullptr;
        size--;
    }
private:
    int size;
    Node* dummy;
};
```


## 206 - 反转链表
* 题目链接：[LeetCode 206 反转链表](https://leetcode.cn/problems/reverse-linked-list/)
* 文章链接：[代码随想录讲解 反转链表](https://programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html)

**看到题目的第一想法**  
这题我做过。就是使用 `previous`。

**看完代码随想录之后的想法**  
思路更清晰了，主要是明白了为什么要返回 `previous`。

**实现过程中遇到的困难**  
还好，这题不难。

---

### 代码
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* curr = head;
        ListNode* prev = nullptr;
        while (curr != nullptr) {
            ListNode* tmp = curr->next;
            curr->next = prev;
            prev = curr;
            curr = tmp;
        }
        return prev;
    } 
};
```

