# LeetCode學習筆記 - 動態規劃 Dynamic Programming - 觀念介紹



## 1. Dynamic Programming 是什麼?



+ 動態規劃，又稱為DP
+ 透過把原問題切成多個相對簡單處理的子問題，來解決複雜問題的一種方法
+ Dynamic Prgramming = 切割和征服(計算、處理)+ 記憶(存儲): 動態規劃的執行過程，就是不斷地讀取數據、處理數據，和存儲數據





## 2. 解決的問題



+ 目標結果不容易透過簡單地直接計算來處理，但走到第n步的結果(也就是後面的結果)，可以使用前面的結果來表達呈現，不是從一開始就能像推骨牌一樣，一路計算到結果
+ 動態規劃所解決的問題，前面的關聯性非常低，與可以直接透過一層一層遞進的問題不太一樣
+ 最開始的結果可以直接取得，通常都具有很明確的條件，像是如果sum(N): 1+2+..N，我們帶入sum(1) = 1，可以很明確地得到最開始的那個結果
+ 通常透過遞迴(Recursion)或迴圈來完成



## 3. 適用範圍

+ 當我們的目標問題可以拆成多種或一種重複的子問題
+ 需要將子問題所解出來的結果儲存並重複地使用它們
+ 子問題的解應該要是不可變動的，才能重複使用，不然都要重新計算會造成計算複雜度提升













## Reference

https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92

http://web.ntnu.edu.tw/~algo/DynamicProgramming.html


