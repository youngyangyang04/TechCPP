查看 SYN 队列

就是查看处在 SYN_RECV 状态的进程连接个数

```
netstat -natp | grep SYN_RECV | wc -l
```

查看溢出情况

```
netstat -s
```

预防 SYN 攻击

- 增大半连接队列

- 开启 SYN cookies 算法 

- 减少 SYN+ACK 重传次数

当服务端受到 SYN 攻击时，就会有大量处于 SYN_REVC 状态的 TCP 连接，处于这个状态的 TCP 会重传 SYN+ACK ，当重传超过次数达到上限后，就会断开连接。那我们减少了重传次数，就会加速断开连接，这里可以联想如果在第三次握手失败了之后的场景