# kafka學習筆記

标签（空格分隔）： 消息中間件

---
## 启动kafka ##

 1. 启动kafka服务因为kafka是依赖zookeeper的所以首先要确保zookeeper已经安装并启动。 `kafka-server-start.sh config/server.properties`
 2. 创建topic话题`kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic test`    --replication-factor 是复制的数量                                    --partitions 是分区的数量                                            --topic test 是topic话题的名字
 3. 启动消息生产者`kafka-console-producer.sh --broker-list localhost:9092 --topic test`                                          --broker-list 是节点的意思，我们启动的单个kafka实例则为一个broker，多个则可以组成kafka集群
 4. 启动消息接收者`kafka-console-consumer.sh --boostrap-server localhost:9092 --topic test --from-begining`

## 消息的兩種方式 ##
點對點的消息系統：簡單來說就是生產者發送消息到隊列中，消費者從隊列中取出消息，如圖所示：
![此处输入图片的描述][1]
發佈－訂閱消息系統：同樣都是生產這發送消息到隊列中，消費者從隊列中取出消息，不同的是可以多個消費這同時從隊列中取出消息，類似與我們的公衆號
![此处输入图片的描述][2]

## 整體的結構和概念 ##
![此处输入图片的描述][3]
![此处输入图片的描述][4]
 1. broker：節點的意思，我們啓動的單個kafka實例則爲一個broker,多個則可以組成kafka集羣。
 2. topic：主題的意思，也就是相當與消息系統中的隊列，一個topic中存在多個partition。
 3. partition：分區的意思，partition下面從物理上又可以細分爲多個segment。segment是最小的存儲粒度
 4. partition offset：offset爲消息偏移量，以partition爲單位，即使再同一個topic中，不同的partition的offset也是重新開始計算的。
 5. group：消費者組的意思，一個group中包含多個消費者。
 6. message：消息，成載體，也就是通信的基本單位，producer可以向topic中發送message。
 7. replicas:partition的副本，保證partition的高可用性。
 8. leader:replicas中的一個角色，producer和consumer只跟leader交互。
 9. follower:replicas中的一個角色，從leader中複製數據，作爲leader的一個副本，一旦leader掛了，他就回從followers中選出新的leader繼續提供服務。
 10. controller：kafka集羣中的一個服務器，用來進行leader election和各種failover。
 11. zookeeper：kafka通過zookeeper來存儲集羣中的meta信息等。

## 問題 ##
爲什麼要將topic進行partition分區

    簡而言之：負載均衡+水平擴展


  [1]: https://upload-images.jianshu.io/upload_images/5551927-782afefbdd6eeadc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/960/format/webp
  [2]: https://upload-images.jianshu.io/upload_images/5551927-bea8acb02bbfd602.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/901/format/webp
  [3]: https://upload-images.jianshu.io/upload_images/5551927-e1afc2a1701e49ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/886/format/webp
  [4]: https://images.gitbook.cn/4b558580-cafe-11e8-ba64-19e24fcb4ae1