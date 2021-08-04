# LeetCode 學習筆記 - Dynamic Programming 方法 - LeetCode第53題 - Maximum Subarray 解法



## 1. 題目



![image1](images\image1.PNG)

**題目:**

給定一個整數數組nums，找出其總和最大的連續子數組(必須至少包含一個數字)，並返回其總相加，子數組要是整數數組中的連續部分



## 2. 解法 - 動態規劃 dynamic programming





**討論:**

我們可以使用遍歷的方式重頭開始一直往前來加總做一個比較，用總值加上現在當前遍歷到的值，來尋找最大值，並在過程中一邊找尋一邊更新我們設定的變數:

+ 目前的總數 sub_sum
+ 目前的最大值 sub_max

如何進行更新?

+ 新的總數值就是目前的總數加上下一個遍歷到的數值(x)，並跟x比大小，如果x比前面總數加上x的數值來的高，就直接把新總數更新成x，如果沒有則更新成前面總數加上x的值
+ 新的最大值，就是用目前最大的數值，比上新的總數值，如果新的總數值較大，就更新成新的總數值，反之則繼續使用當前最大值





**解法概念圖:**



![image2](images\image2.png)



![image3](images\image3.png)



![image4](images\image4.png)



```Python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        ## 如果數組為空，就返回0
        if not nums: return 0
        
        ## 數組的長度
        l = len(nums)
        
        ## 初始化 sub_sum 跟 sub_max，直接指定第一個值
        sub_sum = sub_max = nums[0]
        
        for i in range(1, l):
            sub_sum = max(sub_sum + nums[i], nums[i])
            sub_max = max(sub_sum, sub_max)
            
        return sub_max
```

