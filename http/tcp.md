# TCP协议为什么要设计三次握手

1. TCP协议是一种可靠的，基于字节流的，面向连接的传输层协议
   1. 可靠性体现在TCP协议通信的双方的数据传输是稳定的，即便是在网络不好的情况下，TCP都能够保证数据传输到目标端
   2. TCP通讯双方的数据传输是通过字节流来实现的
   3. 面向连接是因为在数据传输之前必须要建立一个连接，然后基于这个连接来进行数据传输
2. TCP是面向连接的协议，在数据传输之前需要建立一个可靠的连接，TCP采用三次握手的方式来实现连接的建立，通信双方需要发送三次请求才能确保一个可靠连接的建立
   1. 第一次，客户端向服务端发送连接请求，并且携带同步序列号SYN
   2. 第二次，服务端收到请求后，发送SYN和ACK
      1. SYN: 表示服务端是一个同步序列号
      2. ACK：表示对前面的客户端这个请求的一个确认，告诉客户端已经收到了请求
   3. 客户端收到服务端请求之后，再一次发送ACK
      1. ACk: 针对服务端连接的一个确认，表示告诉服务端已经收到请求
3. 为何这样设计
   1. TCP是可靠性通讯协议，所以TCP协议的通信双方都必须要维护一个序列号，去标记已经发送出去的数据包，哪些是已经被对方签收的。三次握手就是通行双方相互告知序列号的初始值，为了确保这个序列号被收到，所以双方都需要一个确认的操作
   2. TCP需要在不可靠的网络环境下实现可靠的数据传输，意味着通信双方必须要通过某种手段实现一个可靠的数据传输通道，三次通信是建立这样通道的最小值
   3. 防止历史的重复连接初始化造成的混乱问题，比如在网络环境很差的情况下，客户端连续多次发起建立连接的请求，假设只有两次握手，那么服务端只能选择接受或者拒绝这个连接请求，但是服务端不知道这个请求是不是之前因为网络堵塞而过期的请求，也就是说服务端不知道当前客户端的连接是有效还是无效的