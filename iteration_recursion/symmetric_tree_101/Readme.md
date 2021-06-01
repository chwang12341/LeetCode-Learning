# LeetCode學習筆記 - LeetCode第101題 - Symmetric Tree 對稱樹解法





## 1. 題目



![image1](images1\image1.PNG)

**題目說明:**

給定一個二元樹的根，檢查它是否是自己的鏡像，也就是左右兩邊是對稱其中間的



## 2. 解法



### 遞迴解法



**判斷一個二元樹是否對稱**:

+ 先判斷root是否存在，如果根本沒有root，就直接傳True

+ 檢查左右子樹是否對稱:

  + 檢查兩個的root是否同時存在，同時不存在的情況下值接回傳True，同時存在的情況下要去判斷其值是否相等

  + 同時存在而且值是一樣的，就開始往下對其左右子樹進行判斷比較

    **子樹的比較:**

  + **當**左子樹的右子樹需要對稱於右子樹的左子樹

  + **且**左子樹的左子樹需要對稱於右子樹的右子樹

  + **才能判斷其為對稱二元樹**

    

#### 方法一

```Python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        ## 如果root為空表示整棵樹為空
        if not root:
            return True
        ## 呼叫判斷是否為鏡像的函式，並把root的左右節點帶入判斷
        return self.isMirror(root.left, root.right)
    
    def isMirror(self, l: TreeNode, r: TreeNode) -> bool:
        ## 如果左右節點為空，直接回傳True
        if l == None and r == None: return True
        ## 如果其中一邊為空，一邊不為空，回傳False
        if l == None or r == None: return False
        ## 如果左右邊的節點值不同，就回傳False
        if l.val != r.val: return False
        ## 接著判斷其下一個左右節點是否為對稱，左子樹的左邊要對稱於右子樹的右邊，左子樹的右邊要對稱於右子樹的左邊
        return self.isMirror(l.left, r.right) and self.isMirror(l.right, r.left)
```





#### 方法二





**步驟:**

Step1: 定義一個用來判斷是否為對稱樹的函式(isSymmetric())

Step2: 定義一個用來判斷是否為鏡像的函式

Step3: 如果t1和t2是一個空值，那他們一定對稱，回傳True

Step4: 如果t1和t2，只有一邊為空值，那一定不會是對稱樹，回傳False

**遞迴**

Step5: 判斷t1的值是否等於t2的值

Step6: 判斷t1的左邊是否等於t2的右邊，t1的右邊是否等於t2的左邊



```Python
class Solution:
    ## 判斷是否為對稱樹
    def isSymmetric(self, root: TreeNode) -> bool:
        return self.isMirror(root, root)
    
    ## 判斷是否為鏡像
    def isMirror(self, t1, t2):
        ## 如果t1和t2都沒有，回傳True
        if t1 == None and t2 == None:
            return True
        
        ## 如果t1或t2其中一個有一個沒有，就回傳False，表示不對稱
        if t1 == None or t2 == None:
            return False
        
        ## 如果t1的值等於t2的值，然後t1左邊的節點會等於t2右邊的節點，t1右邊的節點會等於t2左邊的節點，都符合的情況下，就表示其為對稱樹symmetric tree
        return t1.val == t2.val and self.isMirror(t1.left, t2.right) and self.isMirror(t1.right, t2.left)
```



### 迭代解法



解法:

+ 如果root不存在的情況下，就回傳True

+ 宣告一個佇列(Queue)將其左右結點依序放入佇列 - Python會使用dequeue

+ 當如果佇列中還有節點的時候，就使用迴圈來檢查:

  取出兩個節點(l, r)並檢查其是否相等，值不相等就直接回傳False

+ 依序把l.right, r.left, l.left, r.right裝進佇列中

l.right, r.left 和 l.left, r.righ: 這樣放入是因為倆倆應該要是對稱的，也就是我們要檢查是否對稱的節點

+ 當整個迴圈執行完畢，沒有回傳False，就直接回傳True



```Python
## 導入collections套件
from collections import deque
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        ## 如果root為空值，回傳True
        if not root:
            return True
        
        ## 將左右子樹裝進queue中
        q = deque([(root.left, root.right)])
        
        ## 迭代 只要q還有值就繼續
        while q:
            ## 使用l, r來表示左右子樹
            l, r = q.popleft()
            
            ## 如果l, r為空的話，就繼續
            if not l and not r:
                continue
            ## 如果左右邊都有值，且左邊的值等於右邊的值
            if l and r and l.val == r.val:
                ## 就將對應的下一個檢查節點放入，左邊的左邊對稱於右邊的右邊，左邊的右邊對稱於右變的左邊
                q.append((l.right, r.left))
                q.append((l.left, r.right))
            ## 以外的狀況都為False，像是左右邊的值不相等，或是有一邊為空一邊有值等等
            else:
                return False
            
        return True
```





## Reference

https://leetcode.com/problems/symmetric-tree/submissions/



