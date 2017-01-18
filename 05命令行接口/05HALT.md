# HALT

命令：**vagrant halt [name | id]**

这个命令关闭正在运行的Vagrant管理中的虚拟机。

Vagrant首先第一次尝试运行客户机的关机机制。如果失败，或者指定了**—force**标志，Vagrant将直接关闭虚拟机的电源。

如果使用linux类型的客户机，Vagrant将使用**shutdown**命令优雅的关闭虚拟机，而针对不同的操作系统，**shutdown**命令可能存在**$PATH**的不同的路径中，因此，客户虚拟机有义务将**shutdown**命令的正确路径配置在**$PATH**中。

## 选项

- **-f** 或者**—force**  -  不尝试优雅的关闭机器。而是直接关闭虚拟机的电源。