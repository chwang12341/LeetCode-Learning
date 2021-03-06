# LeetCode筆記 - Linked List - 鏈結串列 - 觀念介紹





## 1. 什麼是鏈結串列 Linked List?



**說明:** 為一種常見的基礎資料結構，由很多個節點連結成一種線性的串列，但不會按照線性的順序來存儲資料，而是在每一個]節點中存放下一個節點的指標(Pointer)，用來指向下一個資料的位置



**類型:** 單向鏈結串列、雙向鏈結串列、迴圈鏈結串列



**適用範圍:**

+ 不在意單點的存取操作，不然最好使用List或Array，因為它們可以直接透過索引找到該值，而鏈結串列只存放下一個指標，所以要一個一個找，尋找一個節點或者存取特定位置的節點需要O(n)，而List或Array只要O(1)
+ 需要新增節點的成本較低時，因為它不必按照順序，在鏈結串列中插入節點的時間複雜度可以達到O(1)
+ 要操作的節點最好在開頭或結尾，因為搜尋節點的時間複雜度為O(n)，但是如果是開頭或結尾要新增節點時間複雜度只需要O(1)





### 單向鏈結



開頭為head指向第一個節點，每個節點包含資料，和下一個節點的記憶體位置，如果不為環狀，最後一個節點會連向NIL



![image1](images\image1.png)





### 雙向鏈結 Doubly Linked List



開頭為head指向第一個節點，每個節點中包含資料，上一個節點指標和下一個節點指標，如果不為環狀，最後一個節點會連向NIL





![image2](images\image2.png)





## 2. 實現操作



+ **新增節點**: x = ListNode(val)



+ **插入節點:** 如果要insert在a和b之間

指定下一個節點: x.next = b

指定a的下一個節點為x: a.next = x



+ **刪除節點**: 假設節點的鏈結為 a -> x => b，要刪除x節點

將a的下一個節點位置修正為b: a.next = b



+ **一次讀取所有鏈結的值**

```Python
## 指向第一個節點
all = head
## 當節點不為空的時候
while all:
    ## 印出節點值
    print(a.val)
    ## 抓取下一個節點
    all = all.next
```





## Reference

https://zh.wikipedia.org/wiki/%E9%93%BE%E8%A1%A8

https://hiskio.com/courses/319/lectures/15386




