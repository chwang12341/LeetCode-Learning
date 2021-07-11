# LeetCode 學習筆記 - Binary Search Tree 方法 - LeetCode第700題 - Search in a Binary Search Tree 解法



## 1. 題目



![image1](images\image1.PNG)

 **題目說明:** 

給定一個二元樹的根和一個整數val，在Binary Search Tree中找到值等於val的節點，並傳回以該節點為根的子樹，但如果這個節點不存在，就回傳一個null



## 2. 解法



### 遞迴方法



Step1: 檢查root根節點

+ 根本沒有root，直接回傳root
+ 如果和val值相等，就等於找到了，所以也回傳root



Step2: 如果val值小於root.val根節點值的話，遞迴搜尋左子樹

Step3: 如果val值大於root.val根節點值的話，遞迴搜尋右子樹

```Python
class Solution:
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        ## 如果root不存在或是root的值等於val，都回傳root
        if not root or val == root.val: return root
        
        ## 如果val大於root，就搜尋右子樹
        if val > root.val: return self.searchBST(root.right, val)
       
        ## 如果val小於root，就搜尋左子樹
        if val < root.val: return self.searchBST(root.left, val)
```







### 迭代方法



Step1: 設定n = root，用來當作是檢查點使用

Step2: 當n不等於null的時候，執行迴圈

+ 如果val等於n.val，就表示找到了，直接回傳n
+ 如果val小於n.val，n往左走
+ 如果val大於n.val，n往右走

Step3: 跳出迴圈表示root根節點為空了或是沒有符合val的節點，就回傳n



```Python
class Solution:
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        ## 令n指向root
        n = root
        ## 當n不為空
        while n:
            ## 當n的值等於val，就回傳n
            if n.val == val:
                return n
            
            ## 當val小於n，就讓n往左走
            elif val < n.val:
                n = n.left
                
            ## 當val大於n，就讓n往右
            else:
                n = n.right
        ## n為空的狀況: 1. root為空 2.沒有符合val值得節點
        return n
```



















