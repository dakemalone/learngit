# express的一些解析

标签（空格分隔）： node.js

---

![express的使用][1]


  [1]: http://www.expressjs.com.cn/images/express-mw.png
  get是request请求的的method，'/'是请求的路径，function表示请求执行的一个方法，req == request，res == response ，next == 中间件函数的回调参数，通常称之为‘下一个’。
  
  app.listen(3000,() => console.log('this test application start on port 3000!!!1'))  3000 == 启动的端口，后面的信息将会在控制台打印出来。
