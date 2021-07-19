# LeetCode 學習筆記 - Bitwise Operation 位元運算方法 - LeetCode第136題 - Single Number 解法



## 1. 題目



![image1](images\image1.PNG)

**題目:**

給定一個不為空的整數數組nums，每個裡面的元素會出現兩次，除了其中一個以外，它只會出現一次，我們要找到它



您必須實作出具有線性執行時間複雜度的解決方式，也就是要在O(N)時間複雜度，並且只能使用恆定的額外空間



## 2. 解法



### 討論

XOR位元互斥或的特性

+ A XOR A = 0
+ 0 XOR A = A
+ A XOR 0 = A
+ XOR 具有結合律和交換律的特性，像是A XOR B XOR C == B XOR C XOR A
+ 如果一個數組中僅有一個數是只有一個，那全部進行XOR就會得到答案



### 實作



#### Bitwise Operation 方法

Step1: 令res = 0

Step2: 執行迴圈，讓res對nums[i]執行XOR運算 (^ = nums[i])

Step3: 最後回傳res，即為解

```Python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        ## 初始化res
        res = 0
        
        ## 進行迴圈，對數組中的每個元素執行XOR運算
        for i in nums:
            res ^= i
            
        ## 回傳res
        return res
```





#### 數學Math方法

概念：2 * (a+b+c)  - (a + a + b + c + c) = b 

就會找到在數組中只有一個的元素

```Python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        ## set: 會把數組中的唯一元素列出來 ex. [1,2,3,4,4,2,3] -> {1, 2, 3, 4}
        
        return (2 * sum(set(nums)) - sum(nums))
        
```















