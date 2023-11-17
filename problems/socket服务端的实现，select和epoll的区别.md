### **Socket服务端示例：**

一般来讲，我们要实现socket的时候，有五个关键的的步骤：

- 创建socket：使用`socket()`系统调用创建一个新的socket文件描述符。
- 绑定socket：使用`bind()`系统调用将新创建的socket绑定到一个地址和端口上。对于服务器程序来说，这个地址通常是服务器的IP地址，端口是你希望服务器监听的端口。
- 监听连接：使用`listen()`系统调用使得socket进入监听模式，等待客户端的连接请求。
- 接受连接：当一个客户端连接请求到来时，可以使用`accept()`系统调用接受这个连接，并获取一个新的socket文件描述符，这个描述符代表了服务器与客户端之间的连接。
- 读写数据：通过`read()`和`write()`或者`send()`、`recv()`系统调用在连接上读取或写入数据。

以上就是一个最基本的Socket服务器的工作流程。当然，在实际的应用开发中，根据应用的需要，可能还会使用更多的系统调用和库函数，例如使用`select()`, `poll()` 或 `epoll()` 处理多个并发连接，使用线程或进程来并行处理多个连接等。



一个简单的示例：

```c++
#include <iostream>
#include <string.h> 
#include <sys/socket.h>
#include <netinet/in.h> 

#define MAX_BUFFER_SIZE 4096 
#define PORT 8080

int main() {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int opt = 1;
    int addrlen = sizeof(address);
    char buffer[MAX_BUFFER_SIZE] = {0};
    
    // 创建 socket 文件描述符
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        std::cerr << "socket failed" << std::endl;
        exit(EXIT_FAILURE);
    }
    
    // 绑定 socket 到 localhost 的 8080 端口
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);

    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address)) < 0) {
        std::cerr << "bind failed" << std::endl;
        exit(EXIT_FAILURE);
    }
    
    // 使服务器开始监听，这里我们设定最大待处理连接数为 3
    if (listen(server_fd, 3) < 0) {
        std::cerr << "listen failed" << std::endl;
        exit(EXIT_FAILURE);
    }
    
    while(1) {
        std::cout << "\nWaiting for a connection..." << std::endl;

        // 接受客户端连接
        if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t*)&addrlen))<0) {
            std::cerr << "accept failed" << std::endl;
            exit(EXIT_FAILURE);
        }

        // 清空 buffer
        memset(buffer, 0, MAX_BUFFER_SIZE);
        
        // 读取客户端发送的数据
        int valread = read(new_socket , buffer, MAX_BUFFER_SIZE);
        std::cout << "Client says: " << buffer << std::endl;
    
        // 向客户端发送消息
        send(new_socket , "Hello from server" , strlen("Hello from server") , 0 );
    }

    return 0;
}

```



### select、poll和epoll的区别

当有多个计算机对我们的服务端发起链接请求的时候，我们需要处理这些请求，于是我们就有了这些处理的方法，当然，他们是最常见的，面试常考的

1. select:
   - **select工作方式是轮询检查**用户所关心的**socket是否就绪**，然后进行处理。由于每次调用select都要在用户态和内核态之间进行切换，且需要重新传递数据结构，所以效率较低。
   - **select对socket数量也有限制，默认是1024个**，因为它使用了位图的方式来存储socket信息。
   - select无法扩展到大规模并发连接，主要是因为它采用线性遍历的方式来处理事件，同时每次调用select都需要遍历全部的文件描述符。
2. poll：
   - **poll没有最大文件描述符数量的限制**。在select中，由于它使用了位图的方式来存储文件描述符，所以默认的最大数目是1024。而**poll使用链表来存储**，所以理论上只受限于系统内存。
   - poll提供了更多的事件类型，并且它的事件类型是通过结构体的方式进行传递的，这远比select的位操作要清晰很多。
   - 当文件描述符就绪时，select需要重新设置所有文件描述符，但poll只需要关注那些就绪的文件描述符。
3. epoll
   - **epoll是Linux特有的I/O多路复用机制，相比于select和poll，通过使用基于红黑树的底层数据结构使得epoll更加灵活且没有最大并发限制。**
   - epoll使用一个文件描述符管理多个事件，通过系统调用epoll_ctl注册fd，然后epoll_wait获取已经准备好的描述符。
   - epoll中的系统调用会将所有监听的socket进行逻辑上的分组，应用程序只需要检查已经就绪的socket。这样在实际开发中，可以根据应用程序的实际需求，只监听并处理那些真正需要关注的事件，而无需像select和poll那样每次都进行全量的轮询。
   - epoll的效率比select高，主要体现在大量并发连接的处理上。