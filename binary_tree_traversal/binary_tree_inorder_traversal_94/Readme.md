# LeetCode學習筆記 - 二元樹走訪方法 Binary Tree Traversal - LeetCode第94題 - Binary Tree Inorder Traversal 解題



## 1. 題目



![image1](images\image1.PNG)



說明: 給定一個二元樹的root，回傳一個使用中序走訪 inorder traversal的節點值串列



## 2. 解決方法 - 遞迴



inorder的順序: LDR 左節點 -> 根節點 -> 右節點



要先確定一個結束的條件

+ 當root為None的時候，就return

處理左節點

+ 接下來，如果當root的左節點存在的話，就把左子樹root.left帶入遞迴

+ 並將root的值裝進結果res的串列中

處理右節點

(注意!!不用做將root的值裝進結果res的串列中，因為右節點也會有左右節點，再帶入左節點放值即可)

+ 接下來，如果當root的右節點存在的話，就把右子樹root.right帶入遞迴

全部遞迴執行完畢後，將結果res回傳即可



### 寫法一

```Python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        ## 創建一個串列，用來裝結果
        res = []
        
        ## 執行遞迴
        self.inorderTraversalSearch( root, res)
        return res
        
    def inorderTraversalSearch(self, root, res):
        ## 如果root存在的話
        if root:
            ## 如果左邊存在節點的話
            if root.left:
                ## 就繼續往左邊下面找節點
                self.inorderTraversalSearch(root.left, res)

            ## 將左邊已經沒有節點的節點裝進res中
            res.append(root.val)


            ## 如果右節點有值
            if root.right:
                ## 往右邊走，然後開始對右邊一樣進行找左邊的節點
                self.inorderTraversalSearch(root.right, res)
        ## 當root不存在時 return
        else:
            return
```





### 寫法二

```Python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        ## 創建一個裝結果的串列
        self.res = []
        
        def inorder(root):
            ## 如果root為none就回傳
            if not root:
                return
            ## 如果左邊有節點，就往左邊走
            if root.left:
                inorder(root.left)
            
            ## 如果左邊沒有節點，root也不為None，就把root的值裝入
            self.res.append(root.val)
            
            ## 如果右邊有節點，就往右邊走
            if root.right:
                inorder(root.right)
            
        inorder(root)
        return self.res  
```











## 3. 解決方法 - 迭代



inorder的順序: LDR 左節點 -> 根節點 -> 右節點



Step 1: 宣告res(結果)和stack(用來存放)兩個串列list

筆記: 

+ stack是屬於LIFO Last In First Out， queue是屬於FIFO First In First Out

+ stack為什麼只是用來存放? 因為會有call stack的問題，也就是會有次數限制

Step 2: 宣告一個curr(current)代表當前位置，並將其從root起始位置開始，當curr和stack不為None的時候:

+ 一路不斷將curr的值裝進stack中，並讓curr不斷往其左邊的位置走，直到left不存在的時候
+ 此時將stack進行pop()，進行的結果一定會是最左邊(最後一個裝入stack)的節點，並將它指定給curr
+ 最後將curr的值裝入到res的串列之中
+ 將curr往右邊走一步(curr = curr.right)

上面的方法會使我們每次都能獲得最左邊的那個節點值

當左邊和根取完後，其分支的右子樹會裝進到stack中

因為stack的特性，最後整個走訪的順序會與遞迴解一樣保持 左->根->右的順序

```Python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        ## 創建stack和res兩個串列
        res, stack = [], []
        ## 將curr指定在root位置上
        curr = root
        
        ## 當curr 或是 stack不為空的時候
        while curr or stack:
            ## 當curr不為空的時候
            while curr:
                ## 將curr存進stack中
                stack.append(curr)
                ## 往左邊走
                curr = curr.left
            ## 當已經走到底了 curr為None
            ## 把stack中最後一個節點值彈出，也就是最左邊的節點
            curr = stack.pop()
            ## 將它裝進res中
            res.append(curr.val)
            ## 將curr往右邊走，因為左邊已經沒有節點了
            curr = curr.right
            
        ##當curr 或是 stack為空的時候，也就是沒有節點沒有走訪的時候
        return res
```

















