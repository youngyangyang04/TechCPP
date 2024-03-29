1. **事件驱动与非阻塞I/O**：Nginx的Worker进程内部使用了异步非阻塞的I/O处理方式和事件驱动的机制来处理请求。Nginx可以处理大量并发连接，而且每个Worker进程都可以同时处理多个请求，这意味着Nginx可以支持高并发且高效率。
2. **反向代理和负载均衡**：Nginx可以设置成反向代理服务器，在这种模式下，Nginx可以接收客户端的请求，然后将该请求转发到后端的其他服务器，并将从后端服务器获取的响应返回给客户端。同时，Nginx也提供负载均衡功能，可以根据预设的策略（如轮询、最少连接等）将请求分发到不同的后端服务器。
3. **静态资源服务**：对于静态资源的请求，Nginx可以直接读取磁盘上的静态文件（如HTML、CSS、JavaScript文件或图片等）并返回。
4. **（可选，如果你不了解面试建议不说）Master-Worker架构**：Nginx采用了Master-Worker的模型。在启动Nginx服务时，首先会有一个Master进程被创建出来，在这个Master进程中，会创建多个Worker进程。Master进程主要负责管理Worker进程，包括读取并验证配置信息、创建、绑定套接字然后传递给worker进程、启动、关闭、维护worker进程等。而Worker进程则负责处理实际的请求。