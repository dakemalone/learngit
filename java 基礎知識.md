# java 基礎知識

标签（空格分隔）： 基礎

---

## jvm ##
jvm是一個抽象的計算機，和實際的計算機一樣，它具有指令集並使用不同的儲存區域。它負責執行指令，還要管理數據，內存和寄存器。
1.指令集 2.寄存器 3.類文件的格式 4.棧 5.垃圾回收堆 6.存儲器

## 結構化設計 ##
結構化程序設計的三種基本的設計結構：順序結構、選擇結構、循環結構。

## 面向對象 ##
面向對象是一種優秀程序設計方法，它的基本思想是使用類，對象，繼承，封裝，消息等基本概念進行程序設計

 1. 從世界觀的角度來說，面向對象的基本哲學是認爲世界是由各種各樣的具有自己的運動規律和內部狀態的對象組成的，不同的對象之間相互作用和通信構成了完全的現實世界。
 2. 從法學的角度來說，面向對象的方法是面向對象的世界觀在開發方法中的直接運用。
 3. 從程序設計的角度來說，面向對象的設計程序語言必須有描述對象及其相互之間關係的語言成分。
 
## 面向對象的基本特徵 ##
 1. 封裝 2. 繼承 3. 多態

## java集合 ##
概述：集合類主要負責保存，盛裝其他數據，因此集合類也被稱爲容器類，集合和數組不一樣，數組元素既可以是基本類型的值，也可以是對象（實際是保存對象的引用變量）；而集合只能保存對象（實際上也是保存對象的引用變量）。

分類：集合類主要由兩個接口派生而出，Collection和Map

## 泛型 ##
泛型實例，把一個任意類型的數組放到一個collection集合裏面

    static <T> void fromArrayToCollection(T[] a,Collection<T> c){
        for(T o:a){
            c.add(a);
        }
    }
例子2:

    static <T> void fromCollectionToCollection(Collection<? extends T> a,Collection c){
        for(T o:a){
            c.add(o);
        }
    }
## java獲得鍵盤輸入 ##
Scanner（1.5的新增） 和 BufferRead
## System類 ##
System類代表當前Java程序的運行平臺，程序不能創建System類的對象，所以它提供了一些屬性和方法，允許直接通過System類名調用這些屬性和方法。System提供了代表標準輸入，標準輸出和錯誤輸出的類屬性，並提供一些靜態方法用於訪問環境變量，系統屬性的方法，還提供了一些加載文件和動態鏈接庫的方法

    獲取系統所有環境變量
    System.getenv();
    獲取指定系統環境變量
    System.getenv("JAVA_HOME");
    獲取系統所有屬性
    System.getProperties();
    獲取指定系統屬性
    System.getProperty("os.name");
    
## Runtiem ##
Runtime類代表java程序的運行時的環境，可以訪問jvm的相關信息，如處理器的數量，內存信息等

    獲得java程序關聯的運行時對象
    Runtime rt = Runtime.getRuntime();
    處理器數量:rt.availableProcessors();
    空閒內存數:rt.freeMemory();
    總內存數:rt.totalMemory();
    可用最大內存數:rt.maxMemory();
    運行記事本程序:rt.exec("notepad.exe");
    
## java程序的國際化 ##
java程序的國際化主要通過三個類完成：

    java.util.ResourceBunble:用於加載一個國家，語言資源包
    java.util.Local：用於封裝一個國家/區域，語言環境
    java.text.MessageFormat:用於格式化帶佔位符的字符串
    
## AWT ##
基本組件

 1. button：按鈕
 2. canvas：用於繪畫的畫布
 3. checkbox：複選框組件
 4. checkboxgroup：多組複選框組件
 5. choice：下拉選擇框
 6. frame：窗口
 7. lable：標籤類
 8. list：列表框組件
 9. panel：不能單獨存在的容器類
 10. srcollbar：滑動條組件
 11. srcollpanel：帶滑動條的容器
 12. textarea：多行文本框
 13. textfiled：當行文本框
 
## 註解Annotation ##
三個標準註解：
1.@Override：用來指定方法覆載
2.@Deprecated:用於表示某個程序元素（類，方法）已經過時
3.@SuppressWarnings:抑制編譯器警告
除了三個標準註解，java.lang.Annotation包下還提供了四個Mate Annotation，用於修飾其他的Annotation
4.@Retention:指定該Annotation可以保存多久

    @Retention(value=RetentionPolicy.CLASS):編譯器將註釋記錄在class文件中，當運行java程序時，jvm不再保存註釋，默認值
    @Retention(value=RetentionPolicy.Runtime)..............................................，jvm也會保存註釋，
    @Rentetion(value=RetentionPolicy.Source):編譯器直接丟棄這種策略的註釋。
5.@Target：用於指定被修飾的Annotation可以用於修飾那些程序元素
6.Ducmented：用於指定該元Annotation類將可以被javadoc工具提取成文檔
## 多線程 ##
進程和線程的區別：
    所有運行中的任務通常對應的就是一個進程，當一個程序進入內存中運行，即變成一個進程，進程是系統進行資源分配和調度的一個獨立單位：
1.獨立性：擁有獨立的資源、私有的地址空間。
2.動態性：程序是一個靜態的指令集合，進程是一個動態的指令集合，具有生命週期和不同時間不同的狀態。
3.併發性：多個進程可以在單個處理器上運行並相互之間不影響。
    線程是進程的組成部分，一個進程可以由擁有多個線程，一個線程必須由一個父進程。線程可以擁有自己的堆，程序計數器和局部變量。共享進程的全部資源。
    線程的生命週期的五個狀態：新建new，就緒runnable，運行running，阻塞blocked，死亡dead。
    線程死亡的三種方式：
1.run方法執行完成，線程正常結束
2.線程拋出一個未捕獲的Exception和Error
3.直接調用該線程的stop方法來結束該線程
    ThreadLocal，是Thread Local Variable線程局部變量的意思，也許將它命名爲ThreadLocalVar會更加的合適，功能就是爲了每一個使用該變量的線程都提供一個變量值的副本，使每一個線程都可以獨立的改變自己的副本。
