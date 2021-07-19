# LeetCode 學習筆記 - Binary Search Tree 方法 - LeetCode第98題 - Validate Binary Search Tree 解法



## 1. 題目

![image1](images1\image1.PNG)



**題目:** 給定一個二元樹的根，確定它是否為一個有效的二元搜尋數(Binary Search Tree, BST)







## 2. 解法



### 討論



**針對一個合法的Binary Search Tree(BST) 而言**

+ 執行中序走訪會按照小到大排列
+ 只要我們能記錄前一個節點，就可以在中序走訪的時候進行檢查
+ 或是記錄當前的範圍也可以拿來檢查，但比較麻煩





###  遞迴解法



Step1: 紀錄last作為物件的變數

Step2: 檢查root:

+ 如果不存在，就回傳True
+ 遞迴檢查左邊的節點 -> 如果有問題就回傳False

Step3: 如果self.last存在而且root.val<=last的值，就回傳False，因為last的值是先進入到排序的，中序的跟則是從左而右，從小而大，所以last應該要是最小的

Step4: 把self.last設為root

Step5: 呼叫遞迴，傳入參數root.right(檢查右邊的節點)

a.

```Python
class Solution:
    ## 初始化一個last
    def __init__(self):
        self.last = None
    
    def isValidBST(self, root: TreeNode) -> bool:
        ## 如果根為空，符合Binary Search Tree
        if not root:
            return True
        
        ## 如果左邊驗證有問題，就回傳False
        if not self.isValidBST(root.left):
            return False
        
        ## 如果last存在且他的值如果大於根的值，就回傳False
        if self.last and root.val <= self.last.val:
            return False
        
        ## 將last設定為root值
        self.last = root
        
        ## 左邊檢查完了，根也好了，再接下來就會是右邊
        return self.isValidBST(root.right)
```







b.

```Python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        ## math.inf:表示無限大
        def validation(node, low = -math.inf, high = math.inf):
            ## 如果根為空，就返回True，因為空的樹符合Binary Search Tree
            if not node: return True
            
            ## 我們拿到的節點，值必須介於其左邊根右邊之間，如果不符合就返回False
            if node.val <= low or node.val >= high: return False
            
            ## 接著進行其左右子樹的檢查
            return validation(node.right, node.val, high) and validation(node.left, low, node.val)
        
        return(validation(root))
```









### 迭代解法

Step1: 檢查root:

+ 不存在的情況下，就回傳True

Step2: 先初始化pre, curr, stack

Step3: 先將最左邊的都塞進去

Step4: 當如果pre存在且curr.val<=pre.val的時候，就回傳False，因為中序走訪是從小到大排列

Step5: 將pre存放curr，然後讓curr往右走(往下一個走)

Step6: 如果離開到迴圈外面了，就表示檢查都沒問題，就回傳True



a.

```Python
class Solution:
    
    def isValidBST(self, root: TreeNode) -> bool:
        ## 如果根節點為空，就返回True
        if not root:
            return True
        ## 初始化 pre, curr, stack
        pre, curr, stack = None, root, []
        
        ## 當curr或是stack不為空的時候，就繼續執行
        while curr or stack:
            while curr:
                ## 把curr裝進stack裡面
                stack.append(curr)
                ## 把curr移向左邊一個節點
                curr = curr.left
            ## 當curr為空了，把stack裡面的元素pop出來
            curr = stack.pop()
            
            ## 如果pre存在，且pre的值大於等於curr，就返回False(因為需要符合左邊要比右邊小)
            if pre and curr.val <= pre.val:
                return False
            ## 把pre指向當前的節點
            pre = curr    
            ## 把curr向右邊移動
            curr = curr.right
        ## 如果都通過審查，就表示為Binary Search Tree
        return True
```









b.

```Python
class Solution:
    
    def isValidBST(self, root: TreeNode) -> bool:
        ## 當根為空，就返回True，因為空樹符合Binary Search Tree
        if not root:
            return True

        ## 初始化一個stack
        stack = [(root, -math.inf, math.inf)]
        ## 當stack不為空的時候就不斷執行
        while stack:
            ## 取得對應的root值、上下限值
            root, low, high = stack.pop()

            ## 如果root為空，就繼續執行
            if not root:
                continue

            ## 把val設為根節點的值
            val = root.val

            ## val要大於low，小於high(介於其左右節點之間)，如果不符合就回傳False
            if val <= low or val >= high:
                return False

            ## 繼續對根的左右節點進行檢查
            stack.append((root.right, val, high))
            stack.append((root.left, low, val))

        return True
```







