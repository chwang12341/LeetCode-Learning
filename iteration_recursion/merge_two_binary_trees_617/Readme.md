# LeetCode學習筆記 - LeetCode第617題 - 遞迴和迭代方法 - Merge Two Binary Trees解法







## 1. 題目



![image1](images\image1.PNG)

**題目說明:**

給定兩個二元樹，並將它們合併，如果有重疊節點的狀況，就將兩個節點的值相加，成為新的節點，如果只有一邊有節點就使用其節點當作新的節點



## 2. 解法



**兩顆二元樹的合併:**

+ 節點同時存在的情況下，兩個節點的值相加
+ 只有存在一邊的節點，就直接使用該節點
+ 節點如果都不存在，表示已經到了尾端，下面不會再有節點了





### 遞迴解法



**解法:**

檢查兩節點

+ 如果都為None，表示不存在，就回傳None
+ 如果只有其中一個節點存在，就回傳該節點
+ 如果都存在，就將兩邊的節點值相加，並合併到t1

執行呼叫進行遞迴

+ 左節點呼叫自身函數進行遞迴並傳入t1.left, t2.left的結果
+ 右節點呼叫自身函數進行遞迴並傳入t1.right, t2.right的結果

最後把root回傳



#### 方法一

```Python
class Solution:
        def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
            ## 當兩邊都為空，救回傳None
            if not t1 and not t2:
                return None
            ## 如果其中一邊為空，就回傳不為空的那邊
            if not t1 or not t2:
                return t1 or t2
                    
            ## 如果兩邊都有值，就加總後傳給t1
            t1.val += t2.val
            ## 遞迴 執行下一個節點:其左右邊
            ## 並將值代入給對應的節點
            t1.left = self.mergeTrees(t1.left, t2.left)
            t1.right = self.mergeTrees(t1.right, t2.right)
                    
            ## 最後回傳t1(因為值都合併到了t1)
            return t1
```

#### 方法二

```Python
class Solution:
        def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
            ## 如果t1為空，回傳t2
            if t1 == None: return t2
            ## 如果t2為空，回傳t1
            if t2 == None: return t1
            ## t1和t2都存在的情況下，建立一個新節點，並將t1和t2加總
            node = TreeNode(t1.val + t2.val)
            ## 遞迴: 執行下一個節點:t1和t2左右邊，並接到新創的節點node底下
            node.left = self.mergeTrees(t1.left, t2.left)
            node.right = self.mergeTrees(t1.right, t2.right)
            
            ## 回傳新創的節點
            return node
```







### 迭代解法



**解法:**

建立一個list當stack使用，並將t1和t2成對裝進

當stack裡面不為空的時候，就執行迴圈:

+ 取出一組節點t
+ (等於t2)t[1]為None的時候，就continue(因為只要採用t1就行)
+ 如果都存在，就將值加總到t[0]，也就是t1上

檢查t[0].left(檢查左邊):

+ 如果為None，就將t[1]直接接上去(也就是當t1為None，直接使用t2的節點)

+ 否則就將t[0].left, t[1].left成對裝入到stack中

檢查t[0].right(檢查右邊)

+ 如果為None，就將t[1]直接接上去(也就是當t1為None，直接使用t2的節點)

+ 否則就將t[0].right, t[1].right成對裝入到stack中

最後只要將t1(也就是t[0])回傳



**補充:**

+ queue: 先進先出

+ stack: 後進先出

```Python
class Solution:
        def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
            ## 如果t1為空，直接回傳t2
            if t1 is None:
                return t2
            ## 創建一個list，來當stack用
            stack = []
            ## 將t1和t2裝入
            stack.append((t1, t2))
            
            ## 迭代
            ## 當stack中還有值，不為空
            while stack:
                ## 取得stack中的值
                t = stack.pop()
                ## 如果t2為空，就繼續
                if not t[1]:
                    continue
                
                ## 如果都有值，就相加合併到t1中
                t[0].val += t[1].val
                
                ## 檢查t1左邊的節點，如果為空，直接接上t2左邊的節點
                ## 如果不為空就接下去檢查t1左邊跟t2左邊的節點(迭代)
                if not t[0].left:
                    t[0].left = t[1].left
                else:
                    stack.append((t[0].left, t[1].left))
                
                
                ## 檢查t1右邊的節點，如果為空，直接接上t2右邊的節點
                ## 如果不為空就接下去檢查t1右邊跟t2右邊的節點(迭代)               
                if not t[0].right:
                    t[0].right = t[1].right
                else:
                    stack.append((t[0].right, t[1].right))               
            ## 由於都合併到了t1，所以回傳t1
            return t1
```





