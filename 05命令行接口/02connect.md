# CONNECT

---

命令：**vagrant connect NAME**

这个连接命令是开启共享环境的[共享命令]()的补充，你可以在[Vagrant 共享这一节]()了解到更多关于Vagrant共享的细节。

以下是这个命令可以使用的标志。

## 选项：

- **--disable-static-ip** - 连接命令可以不会快速启动一个小的虚拟机来创建一个静态的IP地址以便访问，当指定这个标志，访问连接的唯一方法是使用SOCKS 代理地址。
- **--static-ip IP** - 指定连接使用的静态IP地址。默认情况下，Vagrant连接使用的ip地址在172.16.0.0/16空间内。
- **--ssh** - 通过SSH连接到**vagrant share --ssh**共享的环境。