

# LeetCode筆記 - 線性搜尋 Linear Search 和 二元搜尋 Binary Search - 觀念介紹







## 1. Linear Search 是什麼?



+ 按照集合中的元素，重頭到尾找尋是否是我們要的元素
+ 不在乎元素是否有按照大小排序，因為會從第一個開始一個一個搜尋，是一個非常直覺的方式，但對於大型數據而言非常沒效率
+ 又稱為循序排序Sequential Search
+ 時間複雜度: O(N)



### 適用範圍

幾乎沒有限制，但是會有搜尋效率的問題





## 2. Binary Search 是什麼?



+ 在一個排好序的集合中搜尋元素，首先會將這個集合中的中位數取出來，將整個集合分成前後段，然後拿這個中位數與我們要查找的目標值比較，如果目標值比較小就取後半段，如果較大就取前半段，然後一樣再取這段中的中位數，再將這段分成新的前後段，然後一樣拿目標值與中位數進行比較，以此方法不斷進行，直到找到目標元素為止
+ 時間複雜度: O(logN)

**筆記: 時間複雜度為每次切半，都除以2，所以為logN**



### 適用範圍:

+ 排好序的集合(升降冪都可以，預設為升冪)
+ 在還沒有排序前的時間複雜度為O(NlogN) -> 要先進行排序才能判斷原本使用的算法是否比Binary Search 差
+ 數據不重複，重複資料像是[1,2,2,4,4,4,6,6,9,10]







圖示舉例:



**STEP 1:** 

![image1](images\image1.png)



**STEP 2:**

![image2](images\image2.png)

**STEP 3:** 

![image3](images\image3.png)



## Reference

https://hiskio.com/courses/319/lectures/15380






