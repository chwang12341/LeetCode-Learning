# LeetCode學習筆記 - Dynamic Programming 方法 - LeetCode第198題&第213題 - House Robber I & II 解法



## 1. House Robber I



### 題目



![image1](images\image1.PNG)

**題目說明:**

您是一名職業的劫匪，計畫著要搶劫街道上的房子，每棟房子都藏有一定金額的錢，然而唯一能阻止你強劫的限制在相鄰的兩棟房子都會有安全系統，如果同一天晚上有鄰近的兩棟房子遭到闖入，它就會自動聯繫警察



給定一個數組nums，裡面代表著每個房子所藏有的金錢數，返回您今晚可以強劫且不驚動警察情況下的最大金額



### 解法



**討論**

+ 如果我們要偷第i棟，那就不能偷第i-1棟

+ 假設我們設定偷到第i棟的最大搶錢金額是rob[i]的話

  rob[i] = max(nums[i] + rob[i-2], rob[i-1])，也就是最大的收益會是，(第i棟的值+偷到i-2棟的值) 或是 (偷到i-1棟的值)，看哪個收益能夠最大

+ 如果只有第一棟 robs[0] = nums[0]
+ 如果有二棟 robs[1] = max(nums[0], nums[1])，就看第一個值大，還是第二個值大



**解法**

Step1: 初始化rob串列，它的長度為nums的長

+ robs[0] = nums[0]，當偷到第1棟，最大的收益為nums的第一個值
+ rob[1] = max(nums[0], nums[1])，當偷到第2棟，最大的收益為nums的第一個值或第二個值，看誰比較大

Step2: 執行迴圈從i=2到l-1: 

+ 使用rob[i] = max(nums[i] + rob[i-2], rob[i-1])來計算從偷到第三棟開始以後的最大收益
+ 最後回傳最後一個值即可，其實就是當已經計算到了nums最後一個的房子了(長度)，就回傳前面最後一個值的計算結果: rob[-1] 或 rob[l-1]就可以了

```Python
class Solution:
    def rob(self, nums: List[int]) -> int:
        ## 計算nums的長度
        l = len(nums)
        
        ## 如果長度為0，表示根本沒有房子，回傳0
        if l == 0:
            return 0
        ## 如果長度為1，表示只有一棟房子，就回傳第一棟房子的金額
        if l == 1:
            return nums[0]
        
        ## 創建一個用來裝我們能搶最大額度的數組，它的大小與nums相等
        rob = [0] * l
        
        ## 初始化: 第一和第二個值， 第一個是當只有一棟房子的時候，只能搶第一棟的錢
        ## 第二個值是當可以有兩棟搶時，我們選擇擁有最大金額的那一棟
        rob[0], rob[1] = nums[0], max(nums[0], nums[1])
        
        ## 迴圈: 因為前兩個值已經初始化好了，所以從第三個值開始，也就是i=2
        for i in range(2, l):
            ## 第i棟能搶的最大金額，要看i-1棟能搶的最大金額，跟第i-2棟能搶的最大金額加上第i棟本身，哪個金錢數量比較多
            rob[i] = max(nums[i] + rob[i-2], rob[i-1])
        ## 回傳最後一個值 
        return rob[-1]
```





## 2. Hosue Robber II



### 題目

![image2](images\image2.PNG)

**題目說明:**

您是一名職業的劫匪，計畫著要搶劫街道上的房子，每棟房子都藏有一定金額的錢，這地方的所有房子都排成一個圓圈，也就是第一間房子是最後一間房子的鄰居，然而唯一能阻止你強劫的限制在相鄰的兩棟房子都會有安全系統，如果同一天晚上有鄰近的兩棟房子遭到闖入，它就會自動聯繫警察



定一個數組nums，裡面代表著每個房子所藏有的金錢數，返回您今晚可以強劫且不驚動警察情況下的最大金額



### 解法



**討論**

1. 第1棟(i=0)和第l棟(i = l-1)會互相影響，也就是不能偷第一棟跟最後一棟，因為他們相鄰

將狀況分開來討論

2. 偷第1棟(i = 0): 起始位置會是nums[0]

+ 那最後一棟，第l棟(i = l-1)就不能夠偷
+ 所以我們最多只能偷到倒數第二棟(i = l - 2)，因為房屋數量有可能是奇數或偶數，所以有可能最遠偷到倒數第二棟

3. 不偷第一棟的情況: 起始位置會是0

+ 那我們最多就可以偷到最後一棟(i = l - 1)

偷第一棟跟不偷第一棟的狀況，我們只要找到哪個狀況能夠偷最多錢即可



**解法**

分成兩階段來計算: 偷和不偷第1棟(i = 0)

**偷第1棟:**

+ 初始化prev和curr均為nums[0]，prev和curr相當於rob[i-2]和rob[i-1]，這邊我們使用變數來裝載這兩個值

執行迴圈從i = 2到l - 2:

+ 使用tmp和prev暫時儲存上一個prev和curr後

curr = max(prev, tmp + nums[i])，此時的curr相當於rob[i]，而prev相當於rob[i-1]，而tmp相當於rob[i-2]

+ 將curr紀錄到result中，res = curr

**不偷第1棟:**

+ 初始化prev為0，curr為nums[1]

執行迴圈從i = 2到l - 1: (就可以偷到最後一棟)

+ 使用tmp和prev暫時儲存上一個prev和curr後

curr = max(prev, tmp + nums[i])，此時的curr相當於rob[i]，而prev相當於rob[i-1]，而tmp相當於rob[i-2]



**最後result和curr看哪個值大，就回傳哪個**



```Python
class Solution:
    def rob(self, nums: List[int]) -> int:
        ## 計算nums長度
        l = len(nums)
        ## 當長度為0，回傳0
        if l == 0:
            return 0
        ## 當長度為1，回傳nums[0]
        if l == 1:
            return nums[0]
        
        ## 當不偷第一棟的情況: result = rob[l-1]
        ## rob[i] = max(nums[i] + rob[i-2], rob[i-1])
        ## 初始化 previous & current
        prev, curr = 0, nums[1]
        for i in range(2, l):
            ## 將tmp裝前一個prev，prev裝前一個curr
            tmp, prev = prev, curr
            curr = max(nums[i] + tmp, prev)
        ## 將最後一個curr值傳給result
        result = curr
        
        
        ## 當偷第一棟的情況: result = rob[l-2]
        ## 初始化: previous & current
        prev, curr = nums[0], nums[0]
        for i in range(2, l-1):
            ## 將tmp裝前一個prev，prev裝前一個curr
            tmp, prev = prev, curr
            curr = max(nums[i] + tmp, prev)
            
        ## 比較兩種情況誰偷的錢比較多，就回傳誰
        return max(result, curr)
```























