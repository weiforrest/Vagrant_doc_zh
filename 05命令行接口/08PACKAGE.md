# PACKAGE

命令：**vagrant package [name | id]**

这条命令打包当前的*Virtualbox*虚拟机环境到可重用的容器中。这条命令只能在虚拟机管理器支持的前提下。未来的某个Vagrant版本将支持为其他的虚拟机管理器分配打包地址，但现在他们只能手动处理。

## 选项

- **—base NAME** - 指定打包基于的VirtualBox管理的虚拟机。**NAME**应为VirtualBox的图形界面中的虚拟机名称或者虚拟机的UUID。
- **—output NAME** - 将打包的结果命名为**NAME**，默认下，命名为**package.box**。
- **—include x,y,z** - 添加文件到打包的容器中。通常被用来打包Vagrantfile文件以便执行额外的操作。
- **—vagrantfile FILE** - 指定打包容器使用的Vagrantfile，当打包的容器使用时，将作为Vagrantfile 的加载序列。

> **一个比较常见的错误观念**是 **—vagrantfile**选项将打包一个Vagrantfile，作为打包容器在执行**vagrant init**时使用。并不是这样的，而是的容器被使用时，Vagrantfile将被作为Vagrant加载操作加载并读取。了解更多的细节，请阅读[Vagrantfile 加载序列]()。