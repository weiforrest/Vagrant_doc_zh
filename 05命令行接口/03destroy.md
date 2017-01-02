# DESTORY

---

命令：**vagrant destroy [name | id] **

这条命令停止Vagrant管理中的运行中的虚拟机，同时销毁所有虚拟机创建时创建的全部资源，在运行完这条命令以后，你的电脑将回到干净的状态，就像你在之前没有创建一样。

如果使用linux类型的客户机，Vagrant将使用**shutdown**命令优雅的关闭虚拟机，而针对不同的操作系统，**shutdown**命令可能存在**$PATH**的不同的路径中，因此，客户虚拟机有义务将**shutdown**命令的正确路径配置在**$PATH**中。

## 选项

- **-f ** 或 **—force** - 在销毁之前不需要确认。

> 销毁命令不会删除**vagrant up** 执行中安装的容器。因此，无论你运行**vagrant destroy**，已经安装在系统的容器已经保存在硬盘中。如果想要回到**vagrant up**之前的状态，你需要运行**vagrant box remove**。
>
> 想要了解更多内容，请阅读**vagrant box remove** 命令。