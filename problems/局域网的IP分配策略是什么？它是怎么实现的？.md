1. 静态IP分配： 在静态IP分配中，网络管理员手动为每台设备指定一个**唯一**的IP地址。这个过程通常涉及到在网络设备（如计算机、打印机等）的设置界面中手动配置IP地址、子网掩码、默认网关以及DNS服务器地址等参数。静态IP分配通常用于确保特定设备始终拥有相同的IP地址，这对于服务器、网络打印机或其他需要稳定IP地址的设备来说非常重要。
2. 动态IP分配： 动态IP分配则是**通过动态主机配置协议自动完成的**。在这种策略下，设备启动时会向网络发送广播消息，请求IP地址信息。局域网中的DHCP服务器接收到请求后，从其配置的地址池中分配一个IP地址给该设备，并将此信息连同子网掩码、默认网关和DNS服务器地址等通过DHCP响应包发送给设备。

实现动态IP分配的步骤一般包括以下几个阶段：

- DHCP发现（DHCPDISCOVER）：客户端发送广播消息，寻找可用的DHCP服务器。
- DHCP提供（DHCPOFFER）：DHCP服务器响应客户端的请求，并提供IP地址租约信息。
- DHCP请求（DHCPREQUEST）：客户端选择接受其中一个提供的IP地址，并再次以广播的方式发送确认请求。
- DHCP确认（DHCPACK）：DHCP服务器确认IP地址租约，并将最终确认信息和其他网络配置参数发送给客户端。

优点和缺点：

- 静态IP分配可以提供稳定性和确定性，便于管理和网络访问控制，但它不够灵活并且难以扩展到大量设备，尤其是当网络规模变化时，手动配置工作量很大。
- 动态IP分配非常灵活，易于管理大量设备，特别适合设备经常变动的网络环境。然而，由于IP地址可能会变化，对于需要固定IP地址的设备（如某些服务器），动态分配可能不是最佳选择。