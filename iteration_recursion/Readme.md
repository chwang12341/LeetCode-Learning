# LeetCode 學習筆記 - 迭代(Iteration)和遞迴(Recursion) - 觀念介紹



## 1. 迭代法(Interation)是什麼?

+ 又稱為疊代，為一個重複回饋的過程，目的是為了接近且到達所需的結果，每一次重複執行的過程稱為一次疊代，每次疊代的output會成為下一次疊代的input

+ 透過迴圈(ex. for, while)來不斷執行某個操作，取代遞迴自己呼叫自己的功用





## 2. 遞迴法(Recursion)是什麼?

+ 同一個函數，不斷反覆地自己呼叫自己
+ 透過不斷呼叫自己的函式，不斷地將帶入的參數化簡，直到得到我們想要的解
+ 實作時通常是先找到問題的規律，然後重複用相同的操作(不斷呼叫自己)來縮減問題範圍，直到能了解細節，並取得最終所需的部分

**遞迴的種類**

+ 直接遞迴(Direct Recursion): 自己的函式直接呼叫自己本身
+ 間接遞迴(Indirect Recursion):: 函式會先呼叫另外一個函式，另一個函式再呼叫原本的函式





**重要觀念:** 

+ 其實就是迭代是透過迴圈來不斷接近並取得結果，而遞迴是用不斷呼叫自己來達成
+ 選擇兩種方法來解決問題前，要先了解遇到的問題是否可以化簡，因為這樣才需要一層一層用一樣的操作找解



## 3. 遞回(Recursion)和疊代(Iteration)求解的差異



| 比較     | 遞迴(Recursion)                                              | 疊代(Iteration)                |
| -------- | ------------------------------------------------------------ | ------------------------------ |
| 求解方式 | 自己呼叫自己                                                 | 使用迴圈化簡                   |
| 實作難易 | 較容易思考解法                                               | 不容易去推導                   |
| 執行速度 | 可能較慢， 因為當每次函式執行一半然後去執行別的函式，回來後需要有位置(ex. 編譯器)去紀錄執行到哪，也就是執行時需要程式的管理，這樣的過程稱為Call Stack | 可能較快，因為不需要Call Stack |
| 限制     | 由於電腦都會設定Call Stack有上限，怕你一直不斷呼叫自己，所以執行是有限制的，在處理很大的數據時，可能會有問題 | 不受限                         |
| 空間     | 由於需要一個地方紀錄(Call Stack)，空間消耗上可能比較多       | 一般情況下消耗較少             |

Call Stack 大家可以參考wiki定義: https://zh.wikipedia.org/wiki/%E5%91%BC%E5%8F%AB%E5%A0%86%E7%96%8A





## 4. 遞迴(Recursion)和疊代(Iteration)方法的適用範圍



+ 在第一次解題時，由於遞迴比較好思考解法，所以是一個不錯的選擇
+ 實務上課程老師建議的是以迭代解法為主，因為效率通常比較好，而且空間消耗上也通常較少，也比較沒有次數限制
+ 使用遞迴方法來解時，一定要注意Call Stack的最大上限，不然就有可能還沒遞迴出結果就停了

使用sys.getrecursionlimit()來取得Call Stack的上限

```Python
import sys
sys.getrecursionlimit()
```

**執行結果**

```
3000
```



## Reference

https://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92

https://zh.wikipedia.org/wiki/%E8%BF%AD%E4%BB%A3

http://simonsays-tw.com/web/Recursion/Iteration&Recursion.html

http://squall.cs.ntou.edu.tw/cprog/content/10c%20power%20x%20raised%20to%20n_bw.pdf



