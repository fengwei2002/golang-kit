
**rpc 是啥**

rpc 远程过程调用，是一种计算机通信的协议，允许调用不用进程空间的程序  
rpc 的客户端和服务端可以在一台机器上面，也可以不在同一台机器上面，程序员使用的时候，就和本地的程序一样，无需关注内部的实现细节 

通常使用的是 基于 http 协议的 restful api 和 rpc 相比，restful api 存在相对统一的标准，兼容性更好，更加通用

支持不同的语言，http 协议是基于文本的，一般具有更加好的可读性，但是存在缺点： 
- restful api 需要- 额外的定义，两端都需要额外的代码来处理，而 rpc 调用更加接近于直接调用  
- 基于 http 协议的 restful 报文多余，承载了太多没有用的信息。而 rpc 通常使用 自定义的协议风格 从而减少报文的数据量
- rpc 可以采用更加高效的序列化协议，将文本转换为二进制进行传输，获得更好的性能 
- rpc 更加灵活，可以更加容易的扩展和继承一些功能 注册中心，负载均衡等

**rpc 框架需要解决什么问题？** 

如果两个机器上面的应用程序需要进行通信，那么首先，需要确定采用的传输协议是什么，  
如果两个应用程序在不同的机器上面，通常使用的是 tcp 或者 http 协议，   
那么如果两个应用程序在同一个机器上面，可以共同使用 unix socket 协议，传输协议确定之后

还需要确定报文的编码格式，比如采用最常用的 JSON 或者 XML，那如果报文比较大，还可能会选择 protobuf 等其他的编码方式，甚至编码之后，再进行压缩。接收端获取报文则需要相反的过程，先解压再解码。


---

在 net/rpc go 语言基础库上

新增了
- 协议价换 protocol exchange
- 注册中心 registry
- 服务发现 service discovery
- 负载均衡 load balance
- 超时处理 timeout processing 
