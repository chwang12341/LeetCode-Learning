## LeetCode 學習筆記 - Linked Lists 方法 - LeetCode第24題 - Swap Nodes in Pairs 解法



## 1. 題目



![image1](images\image1.PNG)

**題目:**

賦予一個鏈結串列 Linked List，交換每兩個鄰近點，然後返回新的串列

我們需要在不修改到鏈結串列中的值的情況下來解決這個題目，也就是只能改動節點自己來解決



## 2. 解法





### 遞迴解



**想法:** 

創建一個新的Linked List，然後每次都從鏈表的最後(遞迴)添加兩個節點，而且這兩個節點與原本的順序是逆序的



**解法概念圖**



![image2](images\image2.png)



```Python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        ## 如果鏈表頭為空，或是鏈表頭下一個節點為空，都返回鏈表頭
        if not head or not head.next: return head
        
        ## 建立一個新的鏈表頭(指向下一個節點)
        new_head = head.next
        ## 將鏈表頭的指向的下一個節點(遞迴)
        head.next = self.swapPairs(head.next.next) 
        ## 逆序: 將後面的節點指向前一個節點
        new_head.next = head
        
        ## 返回新的鏈表
        return new_head
```



### 迭代解



**想法:** 

以兩個節點為一個單位，做到交換位置處理，然後再指向下兩個節點(迭代)，執行一樣的處理



**解法概念圖**

![image2](images\image2.png)

![image4](images\image4.png)

```Python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        ## 鏈表頭為空，或是下一個節點為空，就返回鏈表頭
        if not head or not head.next: return head
        ## 創建pre裝前一個節點
        pre = new_head = ListNode(0)
        
        ## 當head和head的下一個節點都不為空時
        while head and head.next:
            ## 創建一個tmp用來暫存下一個節點
            tmp = head.next
            ## 讓head的下一個節點指向tmp的下一個節點
            head.next = tmp.next
            ## 讓tmp的下一個節點指向head
            tmp.next = head
            ## 讓pre的下一個節點指向tmp
            pre.next = tmp
            ## pre指向head
            pre = head
            ## head往下指向下一個節點
            head = head.next
        
        
        ## 返回新的鏈表
        return new_head.next
```





