# Netty學習記錄

标签（空格分隔）： java後端技術

---

## Overview ##

Netty是Java的高性能IO工具包。 Netty是開源的，因此您可以自由使用它，如果您願意，甚至可以為它做出貢獻
## netty tools ##
netty包含一套優秀的io流工具，例如：http server,https server,tcp server,ucp server,web websocker,in vm pipe.
## installtion ##

    <dependency>
        <groupId>io.netty</groupId>
        <artifacyId>netty-all</artifacyId>
        <version>FIANL</version>
    </dependency>
## internal desgin##
![][1]


  bootstrap:bootstrap類再netty中是爲了引導netty，引導處理包括開始進程，打開socket.
  EventLoopGroup:是一組的EventLoop.
  EventLoop:是一個不斷尋找新事件的循環，但事件發生時，他就會被傳遞到適當的事件處理器.
  SocketChannel:代表一個通過網絡與另一臺計算機的tcp鏈接
  Channel Initializer:當一個SocketChannel被創建時，ChannelInitializer會指定一個ChannelHandler附加到Socket上.
  ChannelPipeline:每一個SocketChannel都有一個ChannelPipeline(管道),管道中有一系列的channelhandler，當eventloop從socketchannel讀取數據時，數據就會被傳遞到管道中的第一個channelhandler.
  Channel:將從socket傳遞來的數據進行處理，也可以把要傳出到socket的數據進行處理.

## channel pipe ##
![channel pipe][2]
 1. Creating an EventLoopGroup
  `EventLoopGroup group = new NioEventLoopGroup();`
 2. Creating a ServerBootStrap
  `ServerBootstrap serverBootstrap = new ServerBootstrap();
serverBootstrap.group(group);
serverBootstrap.channel(NioServerSocketChannel.class);
serverBootstrap.localAddress(new InetSocketAddress("localhost", 9999));`
 3. Creating a ChannelInitializer
  `serverBootstrap.childHandler(new ChannelInitializer<SocketChannel>() {
    protected void initChannel(SocketChannel socketChannel) throws Exception {
        socketChannel.pipeline().addLast(new HelloServerHandler());
    }
});`
 4. Start the Server
 `ChannelFuture channelFuture = serverBootstrap.bind().sync();`
 5. the hello handler
 `public class HelloServerHandler extends ChannelInboundHandlerAdapter {

    @Override
    public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
        ByteBuf inBuffer = (ByteBuf) msg;

        String received = inBuffer.toString(CharsetUtil.UTF_8);
        System.out.println("Server received: " + received);

        ctx.write(Unpooled.copiedBuffer("Hello " + received, CharsetUtil.UTF_8));
    }

    @Override
    public void channelReadComplete(ChannelHandlerContext ctx) throws Exception {
        ctx.writeAndFlush(Unpooled.EMPTY_BUFFER)
                .addListener(ChannelFutureListener.CLOSE);
    }

    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) throws Exception {
        cause.printStackTrace();
        ctx.close();
    }
}`
  [1]: http://tutorials.jenkov.com/images/netty/overview-0.png
  [2]: http://tutorials.jenkov.com/images/netty/channelpipeline-1.png