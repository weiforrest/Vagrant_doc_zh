# 创建一个基础容器(box)

基础容器(base box)作为一个被人熟知的特别的一类，它们只包括最基本的Vagrant功能，它们不是由现存的Vagrant 环境重新打包制作的，这就是被称为基础(base)的原因。

例如，Vagrant 项目组提供的Ubuntu的基础容器。它们是从Ubuntu ISO 的最小安装方式创建的，而不是现有环境的重新打包。

建立一个干净的Vagrant 基础容器，对构建未来的开发环境是非常有用的。Vagrant 项目组希望在将来能够提供更多系统的基础容器。而现在，这页文档将指导你如何创建你自己的基础容器。

> 高级主题！ 创建基础容器是漫长而且乏味的过程，因此不推荐给新的Vagrant使用者。如果你是Vagrant的新手，我们推荐你先使用现存的基础容器。

## 基础容器里面有什么？

基础容器通常只包括最低限度的的Vagrant功能软件集合。比如说，一个Linux容器可能只包括下面几个：

- 软件包管理。
- SSH
- SSH 用户，这样Vagrant才可以连接。
- 可能有 Chef，Puppet等，但不是必须的。

除了这个，每一个管理工具可能需要额外的软件，比如，你使用VirtualBox制作一个基础容器，它需要安装Virtual guest additions，这样你才可以使用共享目录的功能。但是，如果你使用AWS基础容器，就不需要。

## 创建一个基础容器

创建一个基础容器是与虚拟机管理工具有关的，意味着使用VirtualBox，VMware，AWS等等的过程都是不同的，因此，这个文档不是一个创建基础容器的完全指导。

这一页将指导一个创建基础容器的共通之处，但无论如何，也会提供特定的虚拟机管理工具的指导链接。

特定的虚拟机管理工具的指导链接如下：

- [Docker Base Boxes](https://www.vagrantup.com/docs/docker/boxes.html)
- [Hyper-V Base Boxes](https://www.vagrantup.com/docs/hyperv/boxes.html)
- [VMware Base Boxes](https://www.vagrantup.com/docs/vmware/boxes.html)
- [VirtualBox Base Boxes](https://www.vagrantup.com/docs/virtualbox/boxes.html)

## Packer 和Atlas 工具

我们强烈推荐使用[Packer](https://www.packer.io/)来可重复的创建你的基础容器，它同时也是Atlas的自动化创建工具。阅读更多在Atlas的文档以了解[如何使用Packer创建Vagrant容器](https://atlas.hashicorp.com/help/packer/artifacts/creating-vagrant-boxes)。

## 磁盘空间

当你创建基础容器，应该确保分配足够的磁盘空间去保证用户可以正常使用。比如，在VirtualBox中，你应该给动态扩展的磁盘分配一个足够大的容量。给最终的使用者提供足够的灵活性。

如果你创建一个AWS基础容器，不要强行使用AMI分配TB大小的EBS存储。比如，当用户可以这样做以后，但是你应该默认安装临时的驱动，因为他们是免费而且提供大量的磁盘空间。

## 内存

像磁盘空间一样，找到一个合适的内存分配的平衡点是重要的。大多数的虚拟机管理软件，用户可以使用Vagrantfile配置使用的内存大小。所以不要默认的分配太多。如果**vagrant up**使用的时候需要数GB的内存，那么将会是糟糕的用户体验(令人震惊的)。相反，选择一个较低的值，比如512MB，它足够vagrant运行，但是在我们需要的时候也容易扩大它。

## 外围设备(声卡，USB等)

在基础容器中关闭这些并不是很必须的硬件，比如声卡和USB控制器。这些对于Vagrant用户来说通常是不需要的，而且他们在大多数情况下也可以很容易的在Vagrantfile中配置添加。

## 用户默认设置

Vagrant的几乎所有方面都可以修改。然而，Vagrant期望一些默认的配置，这些默认配置是你基础容器运行所需要的，如果你希望公开发行你的容器，你应该创建这些默认的设置。

如果你是为了私人使用而创建基础容器，你就不要在尝试下面这些了，因为它们会让你的基础容器暴露在安全风险之下。(可知的用户名，密码，密钥等等。)。

### "vagrant" 用户

默认情况下，Vagrant希望使用"vagrant"用户通过SSH登录虚拟机。这个用户应该使用[不安全的密钥对](https://github.com/mitchellh/vagrant/tree/master/keys),这样Vagrant就可以默认使用SSH登录。同时，虽然Vagrant默认使用密钥对作为认证方式，依然有通过将"vagrant"用户的密码设置为"vagrant"来使用普通的方式登录，这样如果用户需要，他们可以手动登录。

为了配置SSH的不安全密钥对，将密钥的公钥写入"vagrant"用户的**~/.ssh/authorized_keys**文件。注意OpenSSH有着严格的权限机制。因此，你需要确保**~/.ssh**的权限是0700，而authorized_keys文件的权限是0600。

当Vagrant启动容器的时候将查找这个不安全的密钥对，它将自动使用一个随机生成的密钥对替换它，以保障它在运行时的安全。

### Root 密码："vagrant"

Vagrant 并不希望并使用任何root密码。无论如何，使用一个统一的容易记忆的root密码可以让公众在需要的时候，更加方便的修改。

### 无密码的Sudo

这是**十分重要**的。Vagrant的很多考虑都希望默认的用户可以使用无密码的**sudo**配置。这样可以方便Vagrant 配置网络，挂载同步目录，安装软件以及更多。

很多操作系统的最小安装并不会默认包含**sudo**程序，因此，你可能需要通过其他的方法安装sudo。

安装sudo程序以后，你需要配置它(一般使用**visudo**)而允许"vagrant"用户可以无密码的使用sudo。通过在配置文件的最后添加下面一行可以达到目的

```
vagrant ALL=(ALL) NOPASSWD: ALL
```

除外，Vagrant 并在通过SSH连接的时候不默认使用pty或者tty。你需要确保在sudo的配置文件没有**requiretty**在里面，如果有的话，删除它，他可以让sudo可以在没有tty的时候正确的运行。记住你可以通过配置Vagrant来让它可以支持pty，pty可以让你保存这个配置，但是Vagrant默认并不这样做。

### SSH 优化

为了在使用的时保证SSH保持高速，同时不让Vagrant虚拟机连接到网络。需要将SSH服务的配置中的UseDNS设置为no。

这样可以避免因为连接的时候查询DNS而浪费几秒钟。

## Windows 容器

支持的Windows操作系统有:

- Windows 7
- Windows 8
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

Windows Server 2003 和Windows XP 是不被支持的，但是如果你是XP的死忠，[这里](https://stackoverflow.com/a/18593425/18475)可能能帮到你。

### 基本的Windows 配置

- 关闭UAC
- 关闭复杂密码
- 关闭 "Shutdown Tracker"
- 在登录时关闭 "Server Manager"()

除了关闭UAC在控制面板，你同样需要在注册表中关闭它。不同的版本可以不同，但是Windows8/8.1使用下面的命令。它可以允许一些操作，比如自动Puppet安装Vagrant的Windows基础容器。

```
reg add HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System /v EnableLUA /d 0 /t REG_DWORD /f /reg:64
```

### 基本的WinRM 配置

为了打开并配置WinRM，你需要将WinRM服务设置为自动开始和允许未加密的基础认证(很显然这是不安全的)。在Windows的命令窗口运行以下的指令：

```
winrm quickconfig -q
winrm set winrm/config/winrs @{MaxMemoryPerShellMB="512"}
winrm set winrm/config @{MaxTimeoutms="1800000"}
winrm set winrm/config/service @{AllowUnencrypted="true"}
winrm set winrm/config/service/auth @{Basic="true"}
sc config WinRM start= auto
```

### 附加的WinRM 1.1 配置

这些额外的配置是专门为Windows Server 2008(WinRM 1.1)特定的。对于Windows Server 2008 R2, Windows 7 以及更新的Windows版本，你可以忽略这一小节。

1. 确认Windows PowerShell 功能以及安装。
2. 将WinRM的端口号改为5985或者升级为WinRM 2.0

下面的命令可以将WinRM的端口号修改为Vagrant所需要的：

```
netsh firewall add portopening TCP 5985 "Port 5985"
winrm set winrm/config/listener?Address=*+Transport=HTTP @{Port="5985"}
```

## 其它的软件

现在，你已经安装了所有你的基础容器可以和vagrant一起使用所需要的软件。然而，如果你愿意，这里有一些额外的软件可以安装。

我们计划在将来，Vagrant在使用那些管理器时，依旧不自动安装Chef或者Puppet。用户可以使用一个Shell来安装，但是，如果你你想在容器以外使用Chef/Puppet,你将需要在基础容器中安装它们。

安装它们已经超过了本页的内容，但是应该是十分的简单。

此外，随意安装软件和配置你想要的其他软件，会让你想要将它们在基础容器添加为默认的。

## 打包容器

将容器打包成容器文件依赖于具体的管理器。请查看具体的管理器的文档的相关内容。一些管理器的文档链接在本页的开始部分。

## 发布这个容器

如果你愿意，你可以发布这个容器文件。而如果你希望它支持版本，通过单个URL得到不同管理器的版本，发布更新，分析，等功能。我们建议你将它加入到[HashiCorp's Atlas](https://www.vagrantup.com/docs/other/atlas.html)。

你还可以在其上上传公共和私有的容器。

##测试这个容器

假如你是Vagrant的新手，给你一个大概的命令：

```
$ vagrant box add my-box /path/to/the/new.box
...
$ vagrant init my-box
...
$ vagrant up
...
```

如果你使用其他的管理器，在**vagrant up**使用**—provider** 参数指定使用的管理器，如果允许成功，你的容器可用。