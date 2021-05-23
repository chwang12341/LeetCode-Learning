# LeetCode筆記 - Binary Search方法 - First Bad Version 解題筆記



## 1. 題目



![image1](images\image1.PNG)







**題目說明:** 您是一位產品經理，負責領導團隊開發新的產品，然而最後一版的產品沒有通過品質檢測，每個新的版本是基於上一個版本開發而來的，所以當這個版本的品質是差的，下一個版本也會是不好的



假如我們有n個版本 [1,2, ... n]，我們需要找到第一個不好的版，因為從它開始導致後面的版本品質都不好



你將給予一個 API bool isBadVersion(version)，它將回傳版本是不是不好的，並實作一個函數來找到源頭(第一個不好的版本)，我們將盡量簡化調用API的數量





## 2. 實作



一樣設定兩個邊界low, up，分別為第一個元素，和最後一個元素，找尋middle值，但這次不能因為middle是不好的版本，就回傳middle的索引，因為它有可能是繼承了上一個不好的版本，所以要往上找: 

**當middle等於bad version:**

+ 如果middle就是第一個元素: 直接回傳middle

+ 如果middle - 1 不是bad version: 就直接回傳middle
+ 找尋範圍應該為: 1(由於是從第一版開始，所以起始位置是1) ~ mid (為什麼不是middle - 1，因為middle有可能就是第一個不好的版本)
+ 但前面已經有設定檢查middle - 1是不是bad version，所以會將up調整為mid - 1，不需要原本的middle元素

**當middle不是bad version:**

+ 調整找尋範圍: mid + 1 ~ up

**如果都沒有版本壞掉，回傳None**



+ **程式實作**

isBadVersion API是由LeetCode團隊已經提供給我們的



```Python
# The isBadVersion API is already defined for you.
# @param version, an integer
# @return an integer
# def isBadVersion(version):

class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        ## 第一版到第n版
        low, up = 1, n
        
        ## 當low小於up也就是沒有交叉，正常的情況下
        while low <= up:
            middle = (low + up) // 2
            
            ## 當middle是bad version
            if isBadVersion(middle):
            
                ## 如果middle就是第一版或是middle前面一個版本不是bad version，就直接回傳middle
                if middle == 1 or not isBadVersion(middle - 1):
                    return middle

                ## 如果middle是bad version，就要看它之前的版本
                up = middle - 1
            
            ## 當middle不是bad version
            else:
                low = middle + 1
                
        
        
        ## 當交叉了，表示裡面根本沒有bad version，就回傳一個None
        return None
```









