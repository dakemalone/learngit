# ｋａｆｋａ學習筆記

标签（空格分隔）： 消息中間件

---

## 消息的兩種方式 ##
點對點的消息系統：簡單來說就是生產者發送消息到隊列中，消費者從隊列中取出消息，如圖所示：
![此处输入图片的描述][1]
發佈－訂閱消息系統：同樣都是生產這發送消息到隊列中，消費者從隊列中取出消息，不同的是可以多個消費這同時從隊列中取出消息，類似與我們的公衆號
![此处输入图片的描述][2]

## 整體的結構和概念 ##
![此处输入图片的描述][3]

 1. broker：節點的意思，我們啓動的單個kafka實例則爲一個broker,多個則可以組成kafka集羣。
 2. topic：主題的意思，也就是相當與消息系統中的隊列，一個topic中存在多個partition。
 3. partition：分區的意思，是構成kafka存儲結構的最小單位。
 4. partition offset：offset爲消息偏移量，以partition爲單位，即使再同一個topic中，不同的partition的offset也是重新開始計算的。
 5. group：消費者組的意思，一個group中包含多個消費者。
 6. message：消息，成載體，也就是通信的基本單位，producer可以向topic中發送message。
 
  [1]: https://upload-images.jianshu.io/upload_images/5551927-782afefbdd6eeadc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/960/format/webp
  [2]: https://upload-images.jianshu.io/upload_images/5551927-bea8acb02bbfd602.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/901/format/webp
  [3]: https://upload-images.jianshu.io/upload_images/5551927-e1afc2a1701e49ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/886/format/webp