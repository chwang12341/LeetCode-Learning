

# LeetCode學習筆記 - 如何開始使用LeetCode刷題 - 刷LeetCode初體驗 - LeetCode 第一題 - Two Sum 解法









## 1. LeetCode 網站如何開始刷題?



### Step 1: 打開LeetCode網站，並登入



### Step 2: 點擊Problems

![image1](images\image1.png)





### Step 3: 塞選題目，並挑選出自己想要的分類題目



![image2](images\image2.png)



### Step 4: 挑選好題目，點進去，就可以開始刷題了喔(以Two Sum為例)



![image3](images\image3.png)





## 2. Two Sum 實作





題目: 



Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly\* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.



給一個整數的nums數組和一個目標整數，程式將傳回數組中兩個數字的索引，也就是這兩個數字相加會等於目標整數

您可以假設每個輸入都只有一個解決方法，而且不會重複使用同一個元素，可以按任何順序傳回答案



### 解法一: 暴力解法



**說明:**  先從list中取一個固定的元素，然後開始從它的下一個元素開始一一配對，看是否相加等於目標值，如果沒有，就換下一個元素，以此類推

```Python
def two_sum(nums, target):
    for i in range(len(nums)):
        for j in range(i+1, len(nums)):
            if nums[i] + nums[j] == target:
                return i, j


nums = [1, 2, 3, 4, 5, 6]
target = 10
two_sum(nums, target)
```

**執行結果**

```
(3, 5)
```





**提醒: 暴力解法，雖然說很好理解，但對於程式執行效能而言，是非常不好的選擇喔，除非不得以，不然希望大家能少用暴力解法**



### 解法二: Hash Table 方法 - 雜湊法



**說明:** 建立一個字典來裝載值跟索引，值放在key，索引放在value，當程式開始執行的時候，因為前面hash_table還沒有添加任何數據，所以一定為空，然後nums前面的數據慢慢填入後，到了後面的元素，hash_table裡面也擁有了很多數據了，就有可能會與前面的元素相加等於目標值，此時就可以傳回





#### 方法一

```Python
class Solution:
    def two_sum(self, nums, target):
        hash_table = {}
        for i, num in enumerate(nums):
            t = target - num
            if t in hash_table:
                return [hash_table[t], i]
            ## 在hash table中增加數據(key: 值, value: 索引)
            hash_table[num] = i
        ## 當沒找到任何答案時回傳[-1, -1]
        return [-1, -1]
            
#             print(hash_table)
nums = [1, 2, 3, 4, 5, 6]
target = 10
Solution().two_sum(nums, target)  
```

**執行結果**

```
[3, 5]
```



#### 方法二



```Python
class Solution:
    def two_sum(self, nums, target):
        hash_map = {}
        for i in range(len(nums)):
            if target - nums[i] in hash_map:
                return hash_map.get(target - nums[i]), i
            hash_map[nums[i]] = i
nums = [1, 2, 3, 4, 5, 6]
target = 10
Solution().two_sum(nums, target)    
```



我放在LeetCode上測了一下執行時間，方法一會稍微快一點喔!!







