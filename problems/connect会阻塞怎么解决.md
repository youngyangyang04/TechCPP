当你调用`connect`函数对远程服务器进行连接时，如果使用的是阻塞式套接字，`connect`会一直阻塞到连接成功或者发生错误为止。这可能导致应用程序的其它部分无法执行，尤其是在图形用户界面或需要同时处理多个连接的服务器应用程序中，这可能是不可接受的。为了解决`connect`函数的阻塞问题，可以采用以下几种方法：

1. **使用非阻塞套接字**：
   - 将套接字设置为非阻塞模式，这样`connect`调用将立即返回。如果连接未立即建立，`connect`会返回一个错误码，通常是`EINPROGRESS`，表明连接尝试正在进行中。
   - 接下来，你可以使用`select`，`poll`或`epoll`等函数来监视套接字的状态。当套接字可写时（`select`等的写集合中返回），这通常意味着连接已经建立或者连接尝试失败，此时可以使用`getsockopt`来检查套接字的`SO_ERROR`选项，以确定是否连接成功。
2. **使用异步I/O或事件驱动模型**：
   - 通过异步I/O库（比如Linux的`libaio`或Windows的`IOCP`）或者事件驱动的网络库（比如`libevent`、`libuv`或`Boost.Asio`），可以在不阻塞主线程的情况下执行`connect`。
   - 这些库通常提供了在连接完成时触发的回调机制。
3. **创建辅助线程或进程**：
   - 在单独的线程或进程中执行`connect`调用，这样即使`connect`阻塞，也不会影响主线程或进程的执行。
   - 连接成功后，可以通过线程间通信机制（如信号量、消息队列、事件等）通知主线程或进程。
4. **使用`O_NONBLOCK`与`connect`结合后的特殊处理**：
   - 在某些系统中，对于非阻塞套接字，`connect`可能立即返回`-1`，并设置`errno`为`EINPROGRESS`。在这种情况下，可以使用`select`或`poll`等函数来监视连接是否成功。



下面用代码来举一个例子：我们先将套接字设置为非阻塞，然后尝试连接。如果`connect`返回`EINPROGRESS`错误，我们利用`select`监视套接字的写事件，如果`select`返回后，套接字的写事件被触发，则调用`getsockopt`检查`SO_ERROR`，看是否连接成功。

```c
#include <sys/types.h>
#include <sys/socket.h>
#include <fcntl.h>
#include <unistd.h>
#include <netinet/in.h>
#include <stdio.h>
#include <errno.h>
// ...

int sockfd = socket(AF_INET, SOCK_STREAM, 0);
if (sockfd < 0) {
    perror("socket");
    return -1;
}

// 设置套接字为非阻塞
int flags = fcntl(sockfd, F_GETFL, 0);
fcntl(sockfd, F_SETFL, flags | O_NONBLOCK);

struct sockaddr_in server_addr;
// 设置server_addr的成员变量...
// ...

int result = connect(sockfd, (struct sockaddr *)&server_addr, sizeof(server_addr));
if (result < 0) {
    if (errno == EINPROGRESS) {
        // 连接正在尝试中
        fd_set writefds;
        FD_ZERO(&writefds);
        FD_SET(sockfd, &writefds);
        struct timeval timeout = {5, 0};  // 设置超时时间

        // 使用select等待连接完成或超时
        result = select(sockfd + 1, NULL, &writefds, NULL, &timeout);
        if (result <= 0) {
            // select错误或超时
            perror("select");
            close(sockfd);
            return -1;
        } else {
            int error = 0;
            socklen_t len = sizeof(error);
            // 获取套接字选项
            if (getsockopt(sockfd, SOL_SOCKET, SO_ERROR, &error, &len) < 0) {
                perror("getsockopt");
                close(sockfd);
                return -1;
            }
            // 检查是否有错误发生
            if (error) {
                errno = error;
                perror("connect");
                close(sockfd);
                return -1;
            }
        }
    } else {
        // 连接尝试出错
        perror("connect");
        close(sockfd);
        return -1;
    }
}

// 套接字现在已连接
// ...

close(sockfd);

```

