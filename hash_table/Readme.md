



# LeetCode學習筆記 - Hash Table 雜湊表 - 觀念介紹







## 1. Hash Table 是什麼?



+ 雜湊表，又稱為哈希表

+　根據鍵值(Key)，並透過Hash Function來查詢在記憶體儲存位置的資料結構
+　其實就是一種資料儲存和訪問的技術
+　由成對的(key, value)所構成，在Python中，通常使用字典(Dictionary)來實現，一個Key對應一個value，不會同時有多個相同名稱的Key
+　主要由Keys、Hash Function和Hash Table所構成，Hash Table由N個buckets所組成，而每個bucket又由M個Slots所構成，每個Slot能夠存取一筆數據





## 2. 實作過程(如下圖):

當我們要獲取Jack(**Keys**)的值，我們需要透過Hash Function來計算出Hashing Address(或Home Address)，然後找到 Hash Table中對應的Bucket來獲取籃球(**values**)



![image1](images\image1.png)



## 3. Hash Table的優勢

+ **主要優點: 執行insert/search/delete/modify的時間複雜度皆為O(1)，也就是不管資料量多大都超級快**

(**但當Hash Collision發生時，上面的優點不成立**)

+ Data與排列順序並沒有什麼關係，所以搜尋數據時，不需要事先排序
+ 由於中間有Hash Function，不瞭解它做了什麼運算，很難取得Data，所以安全性和保密性非常高



## 4. Hash Table 應用範圍



+ 數據本身與其排列順序並無關係
+ 沒有重複訪問值的情況(ex. Jack就是對應籃球)
+ 或重複情況下需要統計次數的時候，像是今天Jack可能從體育室拿了好幾次籃球，我們要去統計他拿了幾次
+ 需要在O(1)的時間複雜度下快速地存取DATA時







## 5. Hash Collision是什麼?

不同筆數據，像是(a, b)，經過中間Hash Function的計算後，得到了一樣的Hashing Address，就是H(a) = H(b)





## 6. Python中如何操作Dictionary



+ 創建字典: {} 或 dict()

```Python
## 創立字典
python_dict = {'x': 1, 'y': 4}
python_dict
```

```
{'x': 1, 'y': 4}
```

+ 插入:

```Python
## 插入新數據
python_dict['z'] = 10
python_dict
```

```
{'x': 1, 'y': 4, 'z': 10}
```

+ 訪問值:

```Python
## 訪問數據
print(python_dict.get('z'))
print(python_dict['z'])
```

```
10
10
```

+ 刪除:

```Python
## 刪除一組數據
del python_dict['z']
python_dict
```

```
{'x': 1, 'y': 4}
```





+ 判斷字典中是否存在某key

```Python
## 第一種方法
print(python_dict.__contains__('z'))
## 第二種方法
print('x' in python_dict)
```

```
False
True
```

+ 取得一組一組的key和value: for k, v in python_dict.items():

```Python
## 取得一組一組的key和value
for k, v in python_dict.items():
    print(k)
    print(v)
```

```
x
1
y
4
```





## Reference

**由於這篇是參考我所學習的課程加上網路資源，再經過自己的消化而來，如果有地方原作者覺得不妥，都請馬上與我聯繫喔，我會馬上移除，感謝**

https://hiskio.com/courses/319/lectures/15376

https://zh.wikipedia.org/wiki/%E5%93%88%E5%B8%8C%E8%A1%A8

https://blog.kennycoder.io/2020/02/18/%E8%B3%87%E6%96%99%E7%B5%90%E6%A7%8B%E8%88%87%E6%BC%94%E7%AE%97%E6%B3%95%E7%AD%86%E8%A8%98-Hashing-%E9%9B%9C%E6%B9%8A%E5%8E%9F%E7%90%86%E4%BB%8B%E7%B4%B9/











