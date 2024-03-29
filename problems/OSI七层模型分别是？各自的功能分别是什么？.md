### 1. 物理层

**功能：** 物理层负责数据在物理媒介上的传输，将来自数据链路层的数据帧转换为电信号、光信号或无线信号。它涉及的范围包括电缆类型、接口形状、引脚数量等。

### 2. 数据链路层

**功能：** 数据链路层管理介质访问控制并进行错误检测与纠正。它将Raw位流组织成逻辑结构称为“数据帧”，并在两个相邻节点之间传输这些帧。此层还负责流量控制和帧同步。

### 3. 网络层

**功能：** 网络层负责设备间的数据传输和寻址。它决定数据的路径路由，并使用IP地址和子网划分来导向目标位置。它也处理分组路由、拥塞控制和网络互联问题。

### 4. 传输层

**功能：** 传输层提供端到端的通信服务。它负责数据的分段和重组，并保证数据完整性。主要协议有TCP和UDP，分别提供可靠的连接和不可靠的连接。

### 5. 会话层

**功能：** 会话层建立、管理和终止应用程序之间的会话。它的职责是建立和维护持久的数据通信会话，并在必要时重新启动会话。

### 6. 表示层

**功能：** 表示层负责数据的编码、转换和解压。它确保来自应用层的数据被网络格式化为适合传输的格式，并在达到目标后被恢复原样。它还可以处理加密和解密。

### 7. 应用层

**功能：** 应用层为最终用户提供网络服务接口。它直接支持各种端用户应用，如Web浏览器、Email客户端、远程文件服务等。此层负责识别和建立与远程应用的通信。