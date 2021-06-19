## LeetCode學習筆記 - 二元樹走訪 Binary Tree Traversal - 觀念介紹



## 1. 前言

這邊我們想要了解當儲存好的二元樹，要進行讀取的時候，會怎麼進行讀取的順序



## 2. 二元樹走訪 Binary Tree Traversal 介紹

**遇到問題**

一般情況下，我們在算式中看到乘法或除法，會優先進行計算，因為它們有較高的優先權(先乘除後加減)，而算式中的括號通常用來標記哪些資料要優先計算，但這種情況下如果使用電腦來判讀這樣的中序式公式，執行起來會非常複雜

**解決方法**

但如果使用前序或後續的話，就不需要出現括號，然後乘除也能依照優先順序來排好，這種方式其實就是將算是轉為二元運算樹，來方便電腦進行計算，而如何產生前序和後序的走訪結果(也就是由前序和後續來挑選算式中哪些先被執行計算，並計算出我們要的結果)，就需要靠中序式的算式來繪製出二元運算樹





## 3. 二元樹走訪的種類?





輸出的方法依種類分成: 深度優先搜尋和廣度優先搜尋兩類，它們的不同在節點的輸出順序，深度優先搜尋是會一直往下尋找節點，廣度優先搜尋則是這一層的節點輸出完了，再換下一層



### 深度優先搜尋 DFS(Depth-first Search)



+ 前序走訪(preorder): DLR

執行順序: 根節點 -> 左子樹 -> 右子樹 

![image1](images\image1.png)





+ 中序走訪(Inorder): LDR

執行順序: 左子樹 -> 根節點 -> 右子樹

![image2](images\image2.png)



+ 後序走訪(Postorder): LRD

執行順序: 左子樹 -> 右子樹 -> 根節點

![image3](images\image3.png)







## 廣度優先搜尋 (BFS)Breathe-first Search



+ 層序走訪: Levelorder

順序: 由根節點一層一層往下，並從左至右輸出

![image4](images\image4.png)





## 4. 舉例



這邊有一顆二元樹，分別使用不同二元樹走訪方法來輸出結果



![image5](images\image5.png)



a. 前序 Preorder: DLR 

```[1,2,4,7,5,8,9,3,6,10]```

b. 中序 Inorder: LDR

```[7,4,2,8,5,9,1,3,6,10]```

c. 後序 Postorder: LRD

```[7, 4, 8, 9, 5, 2, 10, 6, 3, 1]```

d. 層序

```[1,2,3,4,5,6,7,8,9,10]```



**將四則運算加入二元樹後**

![image6](images\image6.png)



a. 前序 Prefix:  波瀾表示法(Polish notation)

```[÷2x7+893-10]```

b. 中序 Infix: 一般情況下的四則運算，需要加上括號

```[(7x28)+(9÷3)-10]```

c. 後序 Postfix: 逆波瀾法(Reverse Polsi notation)

```[7x89+210-31]```



## 5. 二元樹走訪 Binary Tree Traversal 適用範圍



+ 常用在搭配二元搜尋樹的問題(像是中序走訪會剛好按照大小排序)

**由於二元搜尋樹有一個特性: 左邊的節點會小於分節點，分節點會小於右邊的節點，所以中序走訪會剛好按照大小排序**

+ 知道兩種序的輸出結果，我們就可以還原二元樹的形狀

+ 透過遞迴方法可以方便地走訪(但也會受到call back限制，也就是不同機器會限制其遞迴的最大次數)















## Reference

https://ithelp.ithome.com.tw/articles/10243253

https://ithelp.ithome.com.tw/articles/10205571






