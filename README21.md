# Node.js HTTP模块
### 创建静态服务器
~~~
const server=http.createServer()
server.on('request',(request,response)=>{})
server.listen(8888)
~~~
1. http.createServer(options,requestListener),返回<http.server>
2. server是http.server的实例，因此继承了12个事件和方法。
### 获取请求的内容
#### GET请求
1. request.method(获取请求动词)
2. request.url(获取请求路径)
3. request.headers(获取请求头)
#### POST请求
1. request.on('data',fn)(获取消息体)
2. request.on('end',fn)
### request是http.IncomingMessage的实例  
1. 拥有headers,method,url等属性
### response是http.ServerResponse的实例
1. 拥有getHeader  setHeader end  write
2. 拥有statusCode属性