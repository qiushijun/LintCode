 
 
 
## Linked List (16)
**0. [Intersection of Two Linked Lists.java](https://github.com/awangdev/LintCode/blob/master/Java/Intersection%20of%20Two%20Linked%20Lists.java)**      Level: Easy
      
1525664839

给两个 linked list, 问从哪个node开始, 两个 linked list 开始有重复?

#### Basics
- 长短list，找重合点
- 长度不同的话，切掉长的list那个的extra length
- 那么起点一样后，重合点就会同时到达
- Time O(n) * 2, constant space



---

**1. [Add Two Numbers.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Two%20Numbers.java)**      Level: Medium
      

LinkedList都已经反转好了，直接做.
遍历两个l1,l2把carry-on处理好，每次生成一个新node，最后检查carry-on.

跟Add Binary的理解方式一模一样.

注意:
Linked List 没有天然size.
用DummyNode(-1).next来hold住结果.




---

**2. [Add Two Numbers II.java](https://github.com/awangdev/LintCode/blob/master/Java/Add%20Two%20Numbers%20II.java)**      Level: Medium
      

Singly-linked list需要reverse, 用stack.
最终结果要恢复成input list 那样的sequence方向, 用stack一个个pop()刚好就可以做到.

加法都一样:
   1. sum = carry
   2. carry = sum / 10
   3. sum = sum % 10;



---

**3. [Convert Sorted List to Binary Search Tree.java](https://github.com/awangdev/LintCode/blob/master/Java/Convert%20Sorted%20List%20to%20Binary%20Search%20Tree.java)**      Level: Medium
      

Divide and Conquer   
找到mid node

方法1:
用长度来定位mid, 每次找中间点做root, 然后前半段, 后半段分别dfs with length.

方法2: 用快慢pointer
Better: 不用traverse entire linked list

slowPointer = node;
fastPointer = node.next;

然后把root = mid.next     

然后开始sortedListToBST(mid.next.next); //后半段    
mid.next = null;//非常重要，要把后面拍过序的断掉    
sortedListToBST(head); //从头开始的前半段     

最后root.left, root.right merge一下。   



---

**4. [Linked List Cycle.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle.java)**      Level: Easy
      

O(1) sapce: 用快慢指针。一个跑.next, 一个跑.next.next。 总有一次，fast会因为cycle而追上slow。
那个时候其实slow.val = fast.val.

O(n) space: 用HashMap，一直add elements.  如果有重复，那么很显然是有Cycle


---

**5. [Remove Nth Node From End of List.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Nth%20Node%20From%20End%20of%20List.java)**      Level: Medium
      

O(n), one pace, no extra space
找到窗口, 然后平移, 最后pre 和 head之间 skip一个node就好.



---

**6. [Linked List Cycle II.java](https://github.com/awangdev/LintCode/blob/master/Java/Linked%20List%20Cycle%20II.java)**      Level: Medium
      

方法1:
快慢指针, O(1)space.

确认有cycle后, 其实是数学问题:
当head == slow.next时候， head就是cycle starting point.
也就是说，当slow 移动到了那个回溯点，slow.next那个点就刚好是head的那个点...

证明:
1. 假设慢指针走t步, 快指针走快一倍, 也就是2t.
2. 我们假设cycle的长度是Y, 而进入cycle之前的长度为X.
3. 假设慢指针走了m圈cycle, 而快指针走了n圈cycle之后, 两个pointer相遇.
4. 最终在Y cycle里面的K点相遇, 也就是两个指针都在这最后一圈里面走了K 步.
=> 
那么:
t = X + mY + K
2t = X + nY + K
整合公式:
X + K = (n - 2m)Y
这里的m和n不过是整数的跑圈数, 也就是说X和K加在一起, 总归是结束cycle. X 和 K 互补
=> 结论: 当slow/fast 指针在K点相遇后, 再走X步, 就到了cycle的起点, 也就是题目要求的起点.

方法2:
HashMap, O(n) space


---

**7. [Swap Nodes in Pairs.java](https://github.com/awangdev/LintCode/blob/master/Java/Swap%20Nodes%20in%20Pairs.java)**      Level: Medium
      

#### enumurate 
基本原理, 写出来, 然后连线:
pre -> A -> B -> C -> ...
需要一个虚拟 preNode做起始node, 不然无法把后面的node换到开头.

#### 注意
用dummy = pre作为head前一格.
用 `pre.next == null && pre.next.next` 来check是否为NULL.
pre.next.next 保证了至少有一次swap.



---

**8. [Delete Node in a Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Delete%20Node%20in%20a%20Linked%20List.java)**      Level: Easy
      

Given Singlely linked list, 删除一个任意node (不能是head node)

#### Basic
- update node.val
- Link curr.next to curr.next.next



---

**9. [Insertion Sort List.java](https://github.com/awangdev/LintCode/blob/master/Java/Insertion%20Sort%20List.java)**      Level: Medium
      

input一串数字, 需要出sorted output. 每次insert一个数字时, 都要放到正确的sorted的位置

每次insertion的时候, 都从input里面减掉这个数字

#### Linked List
- 把list里面每个元素都拿出来，scan and insert一遍
- Time O(n^2), worst case, 每次放入n个数字里面的element, 刚好都是最大的
- 所以每次要traverse n nodes, 然后走n次

##### 思考方法
- 如果已经有个sorted list, insert一个element进去。怎么做？
- while 里面每个元素都小于 curr, keep going
- 一旦curr在某个点小了，加进去当下这个空隙。



---

**10. [Middle of Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Middle%20of%20Linked%20List.java)**      Level: Easy
      

找Linked List的中间node

- 快慢指针
- 不在乎slow是不是到底，因为fast肯定先到。
- 确保fast, fast.next不是Null就好



---

**11. [Remove Linked List Elements.java](https://github.com/awangdev/LintCode/blob/master/Java/Remove%20Linked%20List%20Elements.java)**      Level: Easy
      

从linked list 里面去掉所有的 target

#### Basics
- 如果match: node.next = head.next;
- 如果不match, node 和 head 一起移动



---

**12. [Palindrome Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Palindrome%20Linked%20List.java)**      Level: Easy
      

#### Reverse Linked List
- Palindrome概念很简单, 但是要在Linkde List random access坐标, 是很难得: 所以需要把一半 ListNode 翻转
- reverse linked list: 遍历接开头
- 用快慢指正找到mid point
- Time O(n), 而且不需要用额外的空间(只是调换半个list的内部顺序), 所以空间O(1)

#### Previous Note
- Palindrome都是要两边回溯相等
- linkedlist不能reverse iterating， 那么就reverse the list, 从中间开花作比较。



---

**13. [Reverse Linked List.java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Linked%20List.java)**      Level: Easy
      

#### Reverse List
- Linked List的基本操作: 每次insert在开头
- 用head来循环所有node
- 不需要额外空间
- Time O(n), Space O(1)



---

**14. [Reverse Linked List II .java](https://github.com/awangdev/LintCode/blob/master/Java/Reverse%20Linked%20List%20II%20.java)**      Level: Medium
      

reverse 一个 linked list 中  [m ~ n] 的一部分.

#### Reverse linked list
- 在基本的reverse linked list 上面 多了一层: 找到front node,  接下来的 [m ~ n] node 需要被reverse
- 只需要reverse中间的部分.
- Reverse的时候: 用一个dummyNode, 这道题里面, 其实就用 nodeFront, 那么 dummy.next 就是整个reversed list.

##### 注意
- 一定要Mark开头的那个mth node, 最后用它接上 剩下node tail. 不然后面的node会断掉

#### Previous notes
- 遍历到M前，
- 存一下那个点，
- 从M开始， for loop， reverse [m~n]。 然后把三段链接在一起。




---

**15. [Merge Two Sorted Lists.java](https://github.com/awangdev/LintCode/blob/master/Java/Merge%20Two%20Sorted%20Lists.java)**      Level: Easy
      

如题

#### Basics
- 小的放前。每次比head大小 
- while过后，把没完的list一口气接上。   
- 一开始建一个node用来跑路, 每次都存node.next = xxx。存一个dummy。用来return dummy.next.



---

