## 什么是ssh

> ssh (SSH-Client) is a program for logging into a remote machine and for executing commands on a remote machine. It is intended to provide secure encrypted communications between two untrusted hosts over an insecure network.  *X11 connections*, arbitrary TCP ports and UNIX-domain sockets can also be forwarded over the secure channel.
>
> ssh connects and logs into the specified hostname (with optional user name). The user must prove his/her identity to the remote machine using one of several methods.
>
> If command is specified, it is executed on the remote host instead of a login shell.
>
> ​                                                                                 ssh - OpenSSH client (remote login program) 帮助手册                                                                            



## 本地动态端口转发

```shell
 -D [bind_address:]port
```

> Specifies a local "dynamic" application-level port forwarding. This works by allocating a socket to listen to port on the local side, optionally bound to the specified bind_address. Whenever a connection is made to this port, the connection is forwarded over the secure channel, and the application protocol is then used to determine where to connect to from the remote machine. Currently the SOCKS4 and SOCKS5 protocols are supported, and ssh will act as SOCKS server. Only root can forward privileged ports. Dynamic port forwardings can also be specified in the configuration file.  

客户端会分配一个socket端口来监听本地请求。当这个端口有连接访问的时候，请求会被重定向进安全通道，并由应用协议来决定远程主机具体访问哪里。



## 应用

已知：主机A由于某些原因，不能访问主机B的网页。但存在主机C，主机A可以访问主机C，而主机C又可以访问主机B。

问题：如何通过主机A访问主机B的网页？

解答：

1. 在主机A的终端，输入如下命令后，回车（输入密码后登录）

   ```shell
   ssh -D 端口 用户名@主机C
   ```

2. 在主机A浏览器中安装代理插件，配置代理信息如下，并启动代理

   ```text
   代理协议：SOCKS5
   
   代理服务器：127.0.0.1
   
   代理端口：SSH -D 对应的端口
   ```

3. 完成上述工作，即可在主机A中访问主机B的网页
