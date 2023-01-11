# Linked List：
链表是一种常见的数据结构，它的结构通常是一个空节点，或者含有一个值和一个指向下一个节点的指针。链表与数组的基本区别有：
**数组(数据是连续的储存在内存里)**
  * 可以使用 index 直接访问某一元素（访问操作时间复杂度O（1））
  * 新元素添加在末尾（添加操作时间复杂度O（1））
  * 删除元素时需要改变被删除元素后面的所有元素位置（删除操作时间复杂度O（n））

**(单)链表(数据并非连续的储存在内存里)**
  * 不能使用 index，访问元素时从head开始一个一个向后查找（访问操作时间复杂度O（n））
  * 新元素添加在末尾，需要先找到最后一个的元素位置（添加操作时间复杂度O（n））
  * 删除元素时需要先找到该元素位置（删除操作时间复杂度O（n））

链表通常使用 **Two Pointers** 和 **Recursion** 这两种方法来解决问题。

### Two Pointers
两个指针指向链表中不同的节点并协同完成任务。
单链表中使用双指针的**注意事项**：
  * 两个指针必须同向而行（从 head 开始向后遍历），因为单链表只能从头开始访问，无法直接获取 tail node 的数据。
  * 两个指针一快一慢，间隔一定距离，间隔根据问题要求而定。

**模版：**
  * 起手初始化两个 pointer 指向 head，p1 和 p2;
  * while 循环遍历链表，循环条件：快指针（p2）在bound 内;
  * 慢指针（p1）移到 next；快指针（p2）移到next.next; **(具体移动位置根据题目而定)**
  * 返回慢指针指向的节点（p1）;

### Recursion
通常递归在链表中的应用使用 Bottom up recursion，使用 stack first in last out 的特性解决关于单链表不能直接从后往前的问题。一般分为三步：
1. 获取子问题的结果
2. 定义在单一递归层操作
3. 返回结果（在递归中，1和3的结果的值的含义必须是一样的）

***递归的主要特点就是层层深入，直到 base case 后再层层返回。所以总是先拿到子问题返回的结果再处理操作。***


### LeetCode 原题
* [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)
```Java
public ListNode middleNode(ListNode head) {
  ListNode p1 = head, p2 = head;
  // 循环条件：快指针走到尾节点时结束循环
  // p2.next != null 用于保证 
  // p2 = p2.next.next 不报错
  while(p2 != null && p2.next != null) {
      p1 = p1.next;
      p2 = p2.next.next;
  }
  return p1;
}
```
该题用双指针找链表的中间节点--> 快的指针每次前进两个节点，慢的每次前进一个节点，这样当快的指针遍历完链表的时候慢指针刚好停留在链表中间节点。有效避免暴力的直接遍历两次链表以获取中间节点。

* [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)
```Java
public ListNode reverseList(ListNode head) {
  // base case, make the tail node be head
  if(head == null || head.next == null) {
      return head;
  }
  // get the result of subproblem, reversedHead = tail node
  ListNode reversedHead = reverseList(head.next);
  // 当前node的next node的next指针指向当前节点，实现链表反转
  head.next.next = head;
  head.next = null;
  return reversedHead;
}
```
