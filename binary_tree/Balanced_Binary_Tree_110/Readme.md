# LeetCode學習筆記 - Binary Tree方法 - LeetCode第110題 - Balanced Binary Tree



## 1. 題目



![image1](images\image1.PNG)





**說明:** 給定一個二元樹，決定它的高度是否平衡



一個高度平衡的二元樹被定義為:

+ **一個二元樹中，每個節點的左子樹和右子樹中的高度不會差超過1**

+ **其左右子樹也為一個平衡二元樹**



**計算平衡樹:**

+ 計算左右子樹的深度: 取一棵樹的高度(深度)，就是把左右子樹高度的最大值 + 1



**檢查是否為平衡樹**

+ 檢查每個分節點的高度(深度)，可以順便檢查其左右子樹是否為平衡二元樹

+ 不為平衡樹的話，可以將結果記錄到上一層的變數，或是傳回-1(因為它已經確定不會是平衡二元樹)





## 2. 實作



### 方法一

```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        def check_depth(root):
            ## 當root為None，回傳0(表示深度為0)
            if root == None:
                return 0
            ## 回傳深度算法 1 + 左右子樹中深度最大的深度值
            return 1 + max(check_depth(root.right), check_depth(root.left))
        
        ## 如果root為None，表示一定為平衡的，因為根本沒有節點
        if root == None:
            return True
        
        ## 計算左右子樹的深度
        left = check_depth(root.left)
        right = check_depth(root.right)
    
        
        
        ## 當左右子樹相減大於1，回傳False表示一定不為平衡樹，如果小於1，就接著判斷左右子樹自身是否也是平衡二元樹，如果都成立就會返回True
        if abs(left - right) > 1:
            return False 
        else:
            return self.isBalanced(root.right) and self.isBalanced(root.left)
```













### 方法二



**解法:**

1. 調用遞迴函式，來不斷檢查計算其節點的高度(深度)

2. 如果root為None，就回傳0(因為不會有深度)

3. 開始計算左子樹和右子樹的深度，並取差值
   + 如果有一邊(單邊: 左子樹或右子樹)其差值超過1，標記為-1，表示有一邊不為平衡二元樹，就直接回傳-1(因為不能為平衡二元樹了)
   + 如果左右子樹相差大於1，也可以直接回傳-1，表示其不為平衡二元樹
   + 否則就傳回1+max(left, right)，也就是計算其最大深度

4. 最終的判斷
   +　如果為-1，就回傳False
   +　如果值大於等於0，就回傳True，表示其為平衡二元樹





**筆記: 大家會不會不太理解為什麼要判斷left或是right為-1嗎，計算深度的函數哪裡有計算它們為-1的可能，深度也不可能為-1啊?**

其實是這樣的當我們計算abs(l - r) >１只要差值大於１，我們都回傳-1，而left跟right正是用check()函數來進行回傳值的，也就是當左右子樹自己裡面的左右邊都不平衡了，整個二元樹，就不會為一個平衡二元樹

```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        ## 撰寫用來檢查深度的函數
        ## -> 標示輸出為int 
        def check_depth(root: TreeNode) -> int:
            ## 如果root為None，就不會有深度
            if root == None:
                return 0
            ## 獲取左右子樹
            right = check_depth(root.right)
            left = check_depth(root.left)

            ## 如果任一左右子樹的深度判斷結果為-1(也就是被判斷其左右邊不平衡 abs(left - right))或是左右邊深度相減超過1，就回傳-1(表示不為平衡二元樹)
            if right == -1 or left == -1 or abs(left - right) > 1:
                return -1

            ## 返回樹的深度
            return 1 + max(left, right)

        
        
        ## 遞迴檢查樹的深度，如果最後結果不為-1就表示為平衡樹
        return check_depth(root) != -1
```





**筆記: 為什麼不用True/False來代表，卻要用-1等數值? 因為可以省掉一個變數空間**



我自己實際測試過兩個方法，方法一使用True/False，方法二則直接使用值來替代，方法二確實較方法一節省空間喔!!







## Reference

https://leetcode.com/problems/balanced-binary-tree/

https://hiskio.com/courses/319/lectures/15423

https://ithelp.ithome.com.tw/articles/10242571





