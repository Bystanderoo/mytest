## 剑指offer52.两个链表得到第一个公共节点

原题链接 https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/

输入两个链表，找出它们的第一个公共节点。

如下面的两个链表：

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

在节点 c1 开始相交。

 

示例 1：

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```c
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```


示例 2：

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```c
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```


示例 3：

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```c
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
```

```
注意：

如果两个链表没有交点，返回 null.
在返回结果后，两个链表仍须保持原有的结构。
可假定整个链表结构中没有循环。
程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。
```

思路解析：

有点像 剑指 Offer 22. 链表中倒数第k个节点 题目，思路一致，都是利用双指针，本题假设链表A和链表B的公共长度为m，

A的前半部分长度为x，B的前半部分的长度为y，则有x+m+y=y+m+x 此时正处于相交点


![ec31dc41bcb43394a14a19273141766](https://user-images.githubusercontent.com/55056723/115579359-acd28900-a2f8-11eb-8a8a-857e969641c5.jpg)


```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode *myheadA=headA;
        ListNode *myheadB=headB;
        while(myheadA!=myheadB){
            if(myheadA==NULL){
                myheadA=headB;
            }else{
                myheadA=myheadA->next;
            }
            if(myheadB==NULL){
                myheadB=headA;
            }else{
                myheadB=myheadB->next;
            }
        }
        return myheadA;
    }
};
```

