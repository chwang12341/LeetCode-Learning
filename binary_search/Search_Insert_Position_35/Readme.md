# LeetCode筆記 - LeetCode第35題 - Search Insert Position 解法







## 1. 題目



![image1](images\image1.PNG)

說明: 給定一個排序好的數組(array)和一個目標值，當目標值有在數組內會傳回一個索引值，如果沒有在數組內，會回傳一個它如果有在數組內會待在的位置索引



## 2. 解法



### 方法一: Linear Search 線性搜尋 - 暴力破解法



**說明:** 從第一個元素開始一個一個找，只要目標值比元素大就往下，直到元素與目標值一樣就傳回index，或是元素比目標值大時，表示數組中並沒有與目標值一樣的元素，所以也就會返回此元素的索引，如果走到最後都沒有，這個目標值就會插在尾端的索引，也就是最後一個索引+1

**時間複雜度:** O(n)



```Python
def linear_search(nums, target):
    for i in range(len(nums)):

        ## 當i還沒到最後一個元素時
        if i < len(nums) - 1:
            ## 當元素與目標依樣時
            if nums[i] == target:
                return i
            ## 當目標值大小介於此元素跟下一個元素中間時
            elif nums[i] < target:
                if nums[i+1] > target:
                    return i+1
           #  當i比第一個元素小時
            elif nums[i] > target:
                return i
            
        ## 當i走到最後一個元素時
        if i == (len(nums) - 1):
            if nums[i] >= target:
                return i
            else:
                return i+1
        
nums = [1, 4, 7, 8, 9]
target = 6
linear_search(nums, target)     
```

**執行結果**

```
2
```









### 方法二: Binary Search 二元搜尋解法





**數組已經排好續的狀況下:**

+ 將兩端設定成low = 0, up = len(array) - 1(數組的長度-1就會是最後一個值得索引)
+ 取中間點: middle = (low + up) // 2，比較array[middle]跟目標值的大小
+ 如果array[middle] == 目標值，回傳middle值
+ 如果array[middle] > 目標值，目標就會在low到middle間(不包含middle)
+ 如果array[middle] < 目標值，目標就會middle(不包含middle)到up間
+ 不斷更新low或up值，然後找到新的middel值，直到array[middle] == 目標值，或是兩者交錯，就是找不到值時，就會回傳low那個位置的索引



```Python
def binary_search(nums, target):
    ## 建立上下界的索引
    low, up = 0, len(nums) - 1
    
    ## 當low沒有與up交叉的時候
    while low <= up:
        middle = (low + up) // 2
        if nums[middle] == target:
            return middle
        ## 當target小於中位數，調整up值，變成middle - 1
        elif nums[middle] > target:
            up = middle -1
        ## 當target大於中位數，調整low值，變成middle + 1
        elif nums[middle] < target:
            low = middle + 1
    ## 調整直到low與up交叉了
    return low
            
nums = [1, 4, 7, 8, 9]
target = 10
binary_search(nums, target)       
```

**執行結果**

```
5
```









