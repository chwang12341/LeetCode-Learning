# LeetCode 學習筆記 - Bitwise Operation 位元運算 - 基礎觀念介紹



## 1. Bitwise Operation是什麼?

+ 位元運算是程式設計中隊位元型態或是二進位數所進行的一元或二元操作，而我們所使用的整數就是以二進位的方式儲存在電腦中
+ 所以位元運算算是對整數進行二進位形式的運算

+ 在過去非常古老的微處理器上，位元運算會加減運算來的快一點，而對於乘法除法運算則是會快非常多
+ 但在現今的架構中，位元運算會跟加減法運算一樣快，但還是會比乘法運算來的快

參考: https://zh.wikipedia.org/wiki/%E4%BD%8D%E6%93%8D%E4%BD%9C



## 2. Bitwise Operation 重要觀念 和 位元運算有哪些?

+ 二進位數中，1代表True，0代表False
+ AND(且)運算: 逐位元計算，當都為1的時候為1(True)，其他的情況都為0(False)
+ OR(或)運算: 逐位元計算，當都為0的時候為False，其他的情況都為1(True)
+ NOT(非)運算: 進行帶正負號的二進位補數計算(所以不是所有情況都是0變1，1變0)
+ XOR(互斥或，Exclusive OR): 當為10或01的情況下為1(True)，其他的情況為0(False)
+ 向右位移 >>: 如果向右位移a位元就在在二進位數的右側刪掉a個位元
+ 向左位移 <<: 如果向左位移a位元就在在二進位數的右側補上a個位元







| 符號 | 說明       | 舉例                     |
| ---- | ---------- | ------------------------ |
| &    | 位元且     | a & b = 0                |
| \|   | 位元或     | a\|b = 10                |
| ^    | 位元互斥或 | a^b = 10                 |
| ~    | 位元非     | ~a = -9                  |
| <<   | 向左偏移   | a << b = 32 (a * (2**b)) |
| >>   | 向右偏移   | a >> b = 2 (a / (2**b))  |



## 3. 範例



構建兩個整數

```Python
## 構建兩個整數
a = 8
b = 2

## 轉換成二進位數
A = bin(a)
B = bin(b)
print('a: ', A)
print('b: ', B)
```

**執行結果**

```
a:  0b1000
b:  0b10
```



AND運算

```Python
## AND
c = a&b
print(c)
print(bin(c))
```

**執行結果**

```
0
0b0
```



OR運算

```Python
## OR
d = a|b
print(d)
print(bin(d))
```

**執行結果**

```
10
0b1010
```



XOR運算

```Python
## XOR
e = a^b
print(e)
print(bin(e))
```

**執行結果**

```
10
0b1010
```



NOT運算

```Python
## NOT
print(~a)
print(bin(~a))
```

**執行結果**

```
-9
-0b1001
```



位移

```Python
## 位移
## 左位移 8 << 2: 8 * (2**2)
f = a << b
print(f)
print(bin(f))

## 右位移 8 >> 2: 8 / (2**2)
g = a >> b
print(g)
print(bin(g))
```

**執行結果**

```
32
0b100000
2
0b10
```



## 4. 適用範圍

+ 利用特性來達成特別的操作，像是計算bit位元為1的數量等
+ 當問題有特別要求要使用位元操作的時候
+ 遮罩Mask的計算方法









## Reference

https://zh.wikipedia.org/wiki/%E4%BD%8D%E6%93%8D%E4%BD%9C

http://kaiching.org/pydoing/py-lesson/py0305.html



