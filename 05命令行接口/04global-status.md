# GLOBAL STATUS

---

命令： **vagrant global-status**

这条命令将告诉你所有当前登录用户的Vagrant环境的状态。

> 这条命令并不显示所有的虚拟机状态，因为它的内容是基于缓存。因此，你可能会看到一个过期的状态（虚拟机显示它正在运行，而实际上并没有）。比如，如果你重启你的电脑，但是Vagrant并不知道。添加**prune**运行global status，可以修正错误的条目。

使用ID栏输出的看起来像**a1b2c3**的值，可以在系统的任何地方控制Vagrant虚拟机。任何Vagrant命令都可以使用ID值作为目标控制它（比如**up**，**halt**，**destroy**)。例如：**vagrant destroy a1b2c3**。

## 选项

- **—prune** - 修正所有错误的条目。这将比正常的输出花费更多的时间。

## 没有显示环境

如果你的环境没有被显示，你可能不得不运行在**vagrant destroy** 后运行**vagrant up**。

如果你只是从Vagrant之前的版本升级，现存的环境将不会在global-status中显示，直到环境被销毁并重新重建。