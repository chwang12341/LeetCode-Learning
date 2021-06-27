# LeetCode學習筆記 - LeetCode第102題 - Binary Tree Traversal 方法 - Binary Tree Level Order Traversal 解題



## 1. 題目



![image1](images\image1.PNG)

題目: 給定一個二元樹的根， 回傳使用層序走訪的結果(從左至右，從上層到下層)





## 2. 解決方法



討論: 層序走訪 - 可以先將比較前面(比較淺)的層走完

+ 遞迴解: 可以利用Preorder前序走訪方法(根->左->右)，搭配level代入到遞迴方法中
+ 迭代解: 需另外宣告一個deque或list來進行記錄





### 遞迴方法





Step 1: 需告一個裝結果的串列res，並先將res預先裝入一個`[]`(空的list，用來放置第一個根節點)

Step 2: 撰寫一個helper函式來執行遞迴: (需傳入的參數: 節點、res、level)

+ 什麼時候停止遞迴? 當傳入的節點為None的時候，也就是沒有節點了，就return

Step 3: 如果當前res長度不夠level所需(ex. 當第一層做完了，進入到第二層時，res長度不夠了，其實就是res中還沒有這一層中的資料)

+ 創建一個空的list，並將當前的節點值裝入之後，再將該list附加append到res串列中

Step 4:如果當前res長度夠level所需

+ 就直接將該節點值裝入到res中對應的level位置

Step 5: 接著分別將左右節點代入並進行遞迴(切記: 要將傳入的level + 1，因為節點的左右節點會在下一層)

Step 6: 遞迴全部執行完畢後，回傳res即可



```Python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        ## 宣告一個空的串列，用來裝結果
        res = []
        
        ## 當root為空，就直接回傳res
        if not root:
            return res
        
        ## 裝入用來裝第一層的list，也就是根節點的位置
        res.append([])
        
        
        def helper(n: TreeNode, res: List[List[int]], level: int):
            ## 當節點為None，也就是已經沒有節點了，就回傳
            if not n:
                return
            
            ## 當如果當前res長度不夠level所需，其實就是res中還沒有這一層中的資料)
            if level > len(res) - 1:
                ## 創建新的一層的串列，並將節點值放入
                new_level = [n.val]
                ## 將其裝入到res中
                res.append(new_level)
                
            ## 當res中已經有這一層的節點了
            else:
                ## 直接將節點裝入到這一層中
                res[level].append(n.val)
            
            ## 接著進行其左右節點的操作(往下一層操作)
            helper(n.left, res, level + 1)
            helper(n.right, res, level + 1)
            
        ## 第一次執行遞迴
        helper(root, res, 0)
        
        ## 回傳結果
        return res
```





### 迭代方法





Step 1: 需告一個裝結果的串列res，並先將res預先裝入一個`[]`(空的list，用來放置第一個根節點)

Step 2: 創建一個queue q(Python中使用的方式為deque，FIFO First In First Out的資料結構)

Step 3: 先將q裝入root，res裝入[root.val]根節點值，並將count初始化為1(count: 用來記錄當前那層有多少個節點)

Step 4: 當q中還有節點的時候:

+　宣告一個temp變數值用來裝取count的數值，然後使用這個值來決定這一層的節點數量

+ 接著將count歸零，並創建一個level串列，用來裝入接下來的節點

+ 從q中popleft()出一個節點curr

  + 當curr有左節點的時候:
    + 將其裝入到q中，並遞增count的值(用來計算下一層有幾個節點)
    + 將level串列裝入curr.left的值

  +　當curr有右節點的時候
    +　將其裝入到q中，並遞增count的值(用來計算下一層有幾個節點)
    +　將level串列裝入curr.left的值

說明: 其實level串列就是用來儲存我們要的資料，而q就是用來存我們要進行的下一層節點

Step 5: 當level串列不為空的時候，就將其裝入到res串列中

**如何知道什麼時候該結束執行?**

Step 6: 當level為空的時候，也就是往下一層沒有節點的時候，就可以return了



```Python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        ## 宣告一個串列，用來裝結果
        res = []
        
        ## root為空的時候，直接回傳res
        if root == None:
            return res
        
        ## 創建一個deque，並把第一層根節點放入
        q = deque([root])
        
        ## 當q還有值，也就是還有節點沒有走訪過
        while q:
            ## 宣告一個變數count，用來裝這一層的節點數量
            count = len(q)
            ## 宣告一個level串列，用來裝節點值，也就是我們要的資料
            level = []
            
            ## 執行次數: 這一層的節點數量
            for _ in range(count):
                ## 從左邊一個一個pop出來，符合FIFO的規則
                n = q.popleft()
                level.append(n.val)
                
                ## 當有其左或右節點時
                ## 接著進行其左節點、右節點(往下一層走訪) 由於順序是左至右，所以一定要先左->右
                if n.left:
                    q.append(n.left)
                
                if n.right:
                    q.append(n.right)
                    
            ## 把結果裝進res中
            res.append(level)
            
        ## 回傳結果
        return res
```

