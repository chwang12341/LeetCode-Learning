# LeetCode學習筆記 - Binary Tree方法 - LeetCode第100題 - Same Tree解法



## 1. 題目



![image1](images\image1.PNG)





**說明:** 給定兩個二元樹的根節點 p 和 q，寫一個函式來檢查它們是相同

如果它們在結構上相同，且節點的值也一樣，就會被認為是相同的二元樹







## 2. 實作



### 遞迴方法 Recursion 方法

+ **遞迴說明:** 透過不斷呼叫一樣的函數，來將問題化，並得到最終答案的方法

+　**使用前提:** 需有確定的狀況條件(也就是要設定一個停點，不然會一直無止盡的執行)和前後連結的關係





**作法**

+ 先拿root比較，是否都存在或都不存在，如果都不存在直接回傳True，如果都存在要還要比較直是否相等，如果不相等回傳False，如果相等就要繼續進行左子樹和右子樹的各自比較
+ 如果左子樹與右子樹相等，那這兩棵二元樹就相同



```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        ## 當p和q都為None的時候
        if p == None and q == None:
            return True
        
        ## 當其中之一為None時
        if p == None or q == None:
            return False
        
        ## 如果都不為None，檢查p和q的值是否相同，如果不相同就回傳False
        if q.val != p.val:
            return False
        
        ## Recursion 遞迴調用函式，來檢查下一個左右子樹的節點是否相同(左子樹根左子樹比、右子樹跟右子樹比
        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
```



### 迴歸方法 Iteration 方法



**補充:** 使用collection套件中的deque，deque為類似於列表(list)的容器，它實現了前後兩端快速添加(append)和彈出(pop)的功能



```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

## 導入collections套件中的deque
from collections import deque
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        ## 建立一個檢查的函數
        def check(p, q):
            ## 如果都為None
            if p == None and q == None:
                return True
            
            ## 如果只有其中一邊為None
            if p == None or q == None:
                return False
            
            ## 如果都不為None，但是兩值不相等
            if p.val != q.val:
                return False
            
            ## 如果成功通過上面的條件
            return True
        
        
        ## 建立一個deque來裝p, q
        c = deque([(p, q),])
        ## 當deque中還有值
        while c:
            ## 將p, q值從deque中取出
            p, q = c.popleft()
            ## 檢查p, q是否相等
            if check(p, q) == False:
                return False
            
            
            ## 當p還有值，也就是還沒比到最後一個節點
            if p != None:
                ## 將p, q的左右子樹的下一個節點插入，左子樹與右子樹要分開比較
                c.append((p.right, q.right))
                c.append((p.left, q.left))
                         
        ## 當都比較完了，都沒有問題
        return True 
```







## Reference

https://leetcode.com/problems/same-tree/submissions/









