# LeetCode 學習筆記 - Bitwise Operation 位元運算 - LeetCode第693題 - Binary Number with Alternating Bits 解法



## 1. 題目



![image1](images\image1.PNG)

**題目:**

給定一個正整數，我們要去檢查它是否有交替位: 就是它的位元中相鄰的兩個位是否為不同值(ex. 1010)



## 2. 解法



### 討論

如何檢查相鄰的位元是否都具有不同的值(0 / 1)

+ 使用XOR方法: 執行右移一個位元後，去與自己進行XOR運算，應該會得到全1的bit，因為01進行XOR後得到1

+ 對得到的全是1的結果加1 ，就會得到最前面進了一位1，後面全是0，這樣再與原本的數值進行&且位元運算，就會得到0，如果不是0，就不對



### 解法 1

Step 1: 先將給定的整數n往右移一位，n >> 1

Step 2: 將上面位移的結果n和原本的n執行XOR運算，會得到都為1的位元

Step 3: 把Step2的結果加1

Step 4: 上面運算完後，檢查n(Step2的結果)執行&且運算n+1(Step3的結果)是否為0，如果不是就回傳False，如果是就回傳True



```Python
class Solution:
    def hasAlternatingBits(self, n: int) -> bool:
        '''
        Procedure
        n =            1 0 1 0 1 0 1 0 1
        n >> 1         0 1 0 1 0 1 0 1 0
        n ^ n >> 1     1 1 1 1 1 1 1 1 1
        n              1 1 1 1 1 1 1 1 1
        n + 1        1 0 0 0 0 0 0 0 0 0
        n & (n + 1)  0 0 0 0 0 0 0 0 0 0 
        '''
        n ^= n >> 1
        return n & (n + 1) == 0
```





### 解法 2

不斷對n進行除2的操作，直到n已經為0，且都通過審查，就表示它符合我們要找的整數，回傳True

```Python
class Solution:
    def hasAlternatingBits(self, n: int) -> bool:
        ## divmod 會分別取得除數跟餘數，像是divmod(5, 2)，就會得到2, 1
        n, cur = divmod(n, 2)
        ## 當n不為0，也就是還能被2除
        while n:
            ## 如果餘數cur等於 n % 2，就回傳False
            if cur == n % 2: 
                return False
            ## 接著繼續對n進行divmod操作
            n, cur = divmod(n, 2)
        ## 如果都通過審查了，就回傳True
        return True
```

















