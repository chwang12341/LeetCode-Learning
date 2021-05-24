# LeetCode學習筆記 - Linked List方法 - LeetCode第21題 - Merge Two Sorted Lists解法



## 1. 題目



![image1](images\image1.PNG)



**說明:** 組合兩個排序好的鏈結串列，並回傳一個排好序的鏈結串列，這個新的串列必須是從原先兩個串列切割開來再合併後的結果







## 2. 實作



**Step 1:** 創建一個鏈結串列中的的第一個節點dummy node

**Step 2:** 再創建一個用來遍歷的tmp node

**Step 3:** 當兩個鏈結列都還有節點時(也就是還沒取光時):

+ 比較兩個鏈結串列的節點值，把比較小的節點接到tmp node的下一個節點位置上
+ 然後prev往下一個走(tmp = tmp.next)，被取用到的節點該鏈節串列(兩個鏈節串列中的一個)也要往下一個走，因為此節點已經被用過了

**Step 4:** 反覆進行上面操作，直到其中一個鏈結串列為空，或兩個串列都空的時候停止

**Step 5:** 如果是其中一個鏈結串列為空，那就直接把還未為空的串列直接接上我們的新鏈結串列

**Step 6:** 最後要傳回dummy node的next(為什麼不是傳回tmp，因為tmp已經走到了最後，它會在最後一個節點的前一個節點位置或是要直接接一整串節點的前一個節點，所以不該傳回它)



```Python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        ## 創建一個空的node
        dummy = ListNode(None)
        ## 創建用來遍歷的node
        tmp = dummy
        
        ## 當兩個鏈結列都還有節點時(也就是還沒取光時)
        while (l1 != None) and (l2 != None):
            ## 如果l1比l2小或一樣，就取l1節點接上
            if l1.val <= l2.val:
                tmp.next = l1
                
                ## l1此節點已經用過了，要往下一個走
                l1 = l1.next
            ## 如果l2比較小，就取l2這個節點
            else:
                tmp.next = l2
                l2 = l2.next
            
            ## tmp往下一個節點走
            tmp = tmp.next
            
                
        ## 當其中一方為空就接上另一方剩下的節點，或兩個都沒值就接上None而已
        tmp.next = l1 or l2
        return dummy.next
```





## Reference

https://leetcode.com/problems/merge-two-sorted-lists/submissions/

















