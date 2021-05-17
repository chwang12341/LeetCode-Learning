# LeetCode學習筆記 - 如何開始使用LeetCode刷題 - 刷LeetCode初體驗 - LeetCode 第242題 - Valid Anagram 解法



## 1. 題目



![image1](images\image1.PNG)



**說明:** 給予兩組字符串s和t，當s裡面的擁有的單字和數量與t是一樣的，只是位置可能調換了，就會返回True，否則返回False



## 2. 解法



### 方法一: hash table



**說明:** 記錄好兩組字符串中的所有單字的次數，並存成Python字典(Hash Table 用法)，然後比較即可

**執行步驟:**

首先: 可以先檢查兩組字串是否等長，如果沒有，表示一定不會是，就直接回傳False

接著: 依序將字母和其出現次數記錄於字典之中

如何進行: 預設為0，然後當s有的字母就+1，t有的時候就-1

結果: 如果計數最後為0表示返回True

```Python
def isAnagram(s, t):
    ## 判斷字串長度是否一樣
    if len(s) != len(t):
        return False
    ## 創建一個用來記錄次數的字典
    c_d = {}
    
    ## 將s中所有的元素裝入字典並計算次數，由於c_d一開始裡面並不會有任何key值，如果直接+1會報錯，所以使用.get先創建一個
    ## 然後賦值為0，接著再+1
    for c in s:
        c_d[c] = c_d.get(c, 0) + 1
#     print(c_d)
    
    ## 將t中所有元素取出，並到c_t中找尋對應有的key，將其值減一
    ## 如果元素根本沒有出現在c_t的key中，表示s中沒有此元素，直接回傳False
    ## 如果c_t中已經把這個元素的計數扣到0了，然後t還有還要繼續扣，也直接回傳False
    for c in t:
        if (c not in c_d) or (c_d[c] == 0):
            return False
        else:
            c_d[c] -=1
#         print(c_d)
    return True
    
isAnagram('elephants', 'aestnhple')    
```

**執行結果**

```
True
```









### 方法二: sorted

**說明:** 只要將兩組字符串重新排序，整個字符串就會依a~z的順序排好，同樣的字母就會排在一起，兩組字串都被重新排序，這樣就可以知道它們是否完全一樣了



```Python
def isAnagram(s, t):
    ## 判斷字串長度是否一樣
    if len(s) != len(t):
        return False
    ## 返回經過排序過後的s和t是否一樣
    return sorted(s) == sorted(t)
isAnagram('elephants', 'aestnhple') 
```

**執行結果**

```
True
```





我在LeetCode上面執行，方法二的執行速度較方法一來得快喔!!



### 方法三: Counter



```Python
def isAnagram(s, t):
    from collections import Counter
#     print(Counter(s))
#     print(Counter(t))
    return Counter(s) == Counter(t)
isAnagram('elephants', 'aestnhple')
```

**執行結果**

```
True
```







結果發現第三種方法跑起來更快xd





