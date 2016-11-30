#  概述

我是一个容易放弃的人，本打算完整的翻译全部的文档，但是那些细枝末节实在让我不知怎样去表达用我蹩脚的英语读出的意思。但是就这样放弃也太快了，想到一个折衷的方法，就是把事情说清楚就行。

---

# 为什么使用Vagrant？

Vagrant提供易于配置，传播和移植的的工作环境，它基于行业标准技术，通过一个稳定的流程控制，最大化的帮助你和你的团队提高生产效率与灵活性。

而为了实现它的神奇，Vagrant站在了巨人的肩膀上。虚拟机的环境使用VirtualBox，VMware，AWS，等其他的虚拟机。因此行业标准化的生产工具，诸如：shell 脚本，Chef，Puppet，可以用来自动化安装及配置虚拟机环境。

###  有何益处

如果你是一名开发者，Vagrant一次性的将软件依赖和配置打包到一个持久的环境中，而不用替换那些你过去工作时常用的工具（编辑器，浏览器，调试器等等）。而你或者其他人只要创建一个**Vagrantfile**配置文件，就可以只用一个 **vagrant up** 命令便可以安装配置完成所有你工作需要的。你团队中的其他成员就可以根据相同的配置创建相同的开发环境，无论你是使用Linux，macOS，还是Windows，所有你团队的成员将在相同的环境，相同的依赖和相同的配置下运行代码。对那些只会出现在我的机器上的bug们说再见吧。

如果你是一名运维工程师，Vagrant将提供一个便携统一的环境来测开发并测试运维脚本。你可以快速测试比如shell脚本，Chef 指南，Puppet 模块和使用更多的本地虚拟化技术，比如VirtualBox 或者VMware。同时，在相同配置下，你可以在例如AWS或者RackSpace的云上使用同样的工作流来测试那些脚本。丢掉你为了回收EC2实例的定制脚本，停止为不同的机器分配SSH登录提示符，Vagrant可以让你回归真正的生活。

如果你是一名设计师，Vagrant将自动设置好所有Web App所需要的环境，而且让你专注于你最擅长的设计。当开发者配置好Vagrant后，你不用再担心如何让应用再次运行。不用再去打扰其他的开发者去帮助你去解决你的应用环境问题以继续你的设计。只需要你输入**vagrant up** 命令，即可开始你的设计。

---

# 安装

安装Vagrant是极度简单的，打开[Vagrant  下载页面](https://www.vagrantup.com/downloads.html)，然后下载为你的操作系统选择合适的安装包。并按照你使用的操作系统的标准安装方式安装。

安装器将自动添加 **vagrant** 到你的系统path变量中，以便于在命令行中使用。如果使用的时候并没有找到，请试图重新登录你的系统（对于Windows有时候是非常的有必要)。

> 通过 gem安装？ Vagrant 1.0.x 使用RubyGem作为可选的安装方式。这种安装方式不再被支持。如果你已经通过Rubygems安装了旧版本的Vagrant，请卸载它以便于安装新版本。

> 当心系统的软件包管理器！有些操作系统的发行版在它们的上游软件包仓库中提供Vagrant。请不要使用这种安装方式。因为它们可能缺少依赖或者已经是废弃的版本。如果你通过你的系统软件包管理器安装的，你很可能会遇到这样的问题。请使用我们下载页面提供的官方安装包。

---

## 向后兼容

### 1.0.X版本

Vagrant 1.1+ 版本对Vagrant1.0.X版本不使用插件并且正确的配置文件提供的完整的向后兼容。安装Vagrant1.1版本后，你的1.0.X版本环境可以在没有任何修改的情况下运行，同时依然在运行的虚拟机能够被正确的管理。

这些年以来Vagrant的主要的发行版本，依旧兼容着你的1.0.x版本的配置文件，这个兼容层将依旧会保留在Vagrant up，当然也包括Vagrant 2.0版本。之后该兼容可能依旧保留，但不确定，毕竟创建它意图只是为了这两个版本。

如果你使用任何Vagrant 1.0.x 版本的插件，你需要在升级之前从你的Vagrantfile配置文件中删除它们。Vagrant 1.1+ 使用了新的插件格式，以避免再次发生这种不兼容的情况。

### 1.X版本

并不保证对1.x版本的向后兼容性，同时Vagrantfile配置文件的语法在最终的2.0版本以前都不保证是稳定的。任何有关1.x的向后不兼容都将有清晰的文档。

这跟0.x版本的处理方法类似，实际上，0.x版本只是在整个开发周期引入了少量的向后不兼容，但是这些可能的向后不兼容都被弄清楚了，所以人们并不为此感到惊讶。

2.0版本将带来稳定的Vagrantfile配置文件的格式以保证向后兼容，正如1.0被认为是稳定的一样。

---

## 升级

如果你准备从1.0.x版本升级，请参阅下一个的页面,本页面涵盖了如何从1.x系列版本升级。

从1.x系列升级Vagrant是十分简单的：

1. 下载最新的包。
2. 安装它以替换存在的包。

安装器将正确的覆盖并删除旧的文件，建议在没有任何Vagrant 运行的情况下升级。

注意在最终2.0版本以前，Vagrantfile配置文件的语法都不保证是稳定的。所以尽管那些1.0.x版本的Vagrantfile配置文件已经可以继续使用，但新的Vagrantfile配置文件在最终的2.0版本以前可能有向后不兼容的改变

> 在升级的时候发生问题？请提交你在升级中遇到的问题，升级的过程几乎没有感觉，如果不是这样，我们认为是一个Bug。

---

## 从1.0.x版本升级

从1.0.x版本升级到1.x版本是很简单的。Vagrant向后兼容1.0.x版本，所以你可以简单的通过最新的安装包，使用你操作系统标准的安装方式重新安装以取代之前的版本。

正如之前先后兼容的页面所说，Vagrant 1.0.x版本的插件并不能在1.1+版本下使用，这些插件需要升级以和新的版本的Vagrant一起使用。所以你需要查看下他们是否需要更新，如果不是的话，你不得不在升级之前删除他们。

建议你在升级之前删除所有的插件，然后在依次确认的添加它们。这样可以让整个升级过程得以平滑的处理。

> 如果你的Vagrant 是通过Rubygems安装的，你必须先卸载老的版本，如何再重新安装。Rubygems的安装方式不再被支持。

---

## 从源码安装

从源码安装Vagrant是高级的主题，它只被推荐无法使用官方安装器安装的情况下。这个页面将详细的列出使用源码安装的步骤和前提。

### 安装Ruby

你需要Ruby(>= 2.0)去构建Vagrant。指定的Ruby版本被记录在Vagrant的gemspec中。请参考Github仓库中的vagrant.gemspec,因为它是最新的需求。本指导不会去涉及如何安装和管理Ruby。无论如何，请避开以下的坑：

1. 不要使用系统自带的Ruby，使用一种Ruby版本管理，比如rvm或chruby。

2. 确保你使用的是最新的Rubygems。

3. 确保你安装的Bundler是Vagrant兼容的。

   Vagrant有一个不断改变的bundler限制。当你编译源码的时候，你需要检查**vagrant.genspec**去选择你使用的bundler版本，比如，如果gemspec被指定为1.2.3版本，你就需要安装该版本的Bundler以满足该限制。

   你可以通过以下命令去安装指定版本的bundler

   ```
   gem install bundler -v '1.2.3'
   ```

### 克隆 Vagrant

将Vagrant仓库从Github上克隆到你的机器上：

```Shell
$ git clone https://github.com/mitchellh/vagrant.git
```

然后，cd 进入本地目录，所有的命令都将在这个路径下运行：

```shell
$ cd /path/to/your/vagrant/clone
```

运行bundle 命令，加上需要的版本号以安装依赖：

```shell
$ bundle _1.10_6_ install
```

你现在可以通过从该目录执行bundle exec vagrant 以运行Vagrant。

### 本地使用

为了在其他的工程中使用你已经在本机中安装的Vagrant，你需要创建一个binstub，并把它加入你的路径中。

首先，在Vagrant仓库运行以下命令：

```shell
$bundle --binstub exec
```

它将在**exec/** 下生成相应的文件，包括**vagrant**。你现在可以在你的操作系统中的任何地方指定**exec/vagrant**的完整的路径来使用它:

```shell
$ /path/to/vagrant/exec/vagrant init -m hashicorp/precise64
```

注意你可能收到不支持这样运行Vagrant的警告。你应该听从这些警告。

如果你不想指定全局路径去运行Vagrant（你只想通过简单输入**vagrant**），你可以为你的执行文件创建一个符号链接：

```shell
$ ln -sf /path/to/vagrant/exec/vagrant /usr/local/bin/vagrant
```

当你想切换回官方的版本时，你只需要移除这些符号链接。

---

## 卸载

卸载Vagrant同样非常简单。你可以选择卸载可执行文件，删除用户数据，或者两者都是。这一节将说明如何在各种操作系统中操作。

### 卸载 Vagrant 程序

卸载Vagrant程序将会从你的机器上删除 **vagrant** 执行文件和所有的依赖。卸载以后你依旧可以使用标准的方法重新安装。

#### Windows平台

> 在控制面板中的添加/删除程序中卸载。

#### macOS 平台

```
rm -rf /Applications/Vagrant
rm -f /usr/local/bin/vagrant
sudo pkgutil --forget com.vagrant.vagrant
```

#### Linux 平台

```
rm -rf /opt/vagrant
rm -f /usr/bin/vagrant
```

### 删除用户数据

删除用户数据将删除所有的boxes，插件，许可证文件和Vagrant所存储的状态数据。删除用户数据可以重新初始化Vagrant。

在所有的平台上，通过删除**~/.vagrant.d** 目录删除用户数据。当调试的时候，Vagrant支持团队可能要求你删除这个目录。在删除该目录前，请备份一下。

运行Vagrant将重新自动生成所有运行需要的文件。所以任何时候删除他们都是安全的。

---

# 入门指引

入门指引将贯穿你的第一个Vagrant项目，同时向你展示一下Vagrant提供的主要功能的基本面貌。

如果你好奇Vagrant所提供的便利，你可以阅读"有何益处"这一节。

这个入门指引将以VirtualBox为虚拟机管理器，因为他是免费的，在所有的主流平台可用，同时集成在 Vagrant。在读完该指引以后，不要忘了Vagrant同样可以与其他虚拟机管理器一起使用。

在开始你的第一个项目前，请安装最新版本的 Vagrant。同时因为要使用 VirtualBox 作为我们的虚拟机管理器，也请安装它的最新版。

>更多的书籍？ 如果你想阅读实体书籍，你可能对这本**Vagrant：Up and Running**感兴趣。这本书的作者是Vagrant的开发者，由O'Reilly出版社出版。

### 开始和运行

```shell
$ vagrant init hashicorp/precise64
$ vagrant up
```

在运行以上两个命令以后，你已经有了一个运行在VirtualBox的Ubuntu 12.04 LTS 64-bit的虚拟机。你可以通过**vagrant ssh** 来通过SSH登录你的虚拟机。当你尝试以后，可以通过**vagrant destroy** 销毁这个虚拟机。

现在可以想象你所有的项目都可以通过这样简单的方法处理。通过Vagrant，只需键入 **vagrant up** 将完成你在任何项目上需要做的，安装项目所有的依赖，设置网络或者同步文件夹。然后你就可以在你自己的机器上舒适的继续工作。

接下的指引将带你设置一个更加完整的项目，包括更多Vagrant的功能。

### 下一步

你已经使用Vagrant创建了你的第一个虚拟机环境。请继续阅读,了解更多关于**项目部署**。

---

## 项目部署

第一步创建配置Vagrant项目的**Vagrantfile**配置文件。它的作用有两个：

1. 确认你的项目的根目录。Vagrant中许多配置选项都依赖于这个根目录。
2. 描述项目运行的虚拟机类型和资源，比如你需要的安装的软件和你想要如何去访问虚拟机。

Vagrant 使用内建的 **vagrant up** 命令去初始化目录，为了完成这个开始指引，请在你的终端中输入下面的命令：

```Shell
$ mkdir vagrant_getting_started
$ cd vagrant_getting_started
$ vagrant init
```

以上命令将在你当前目录生成一个**Vagrantfile**文件，如果你想，你可以查看下这个文件的内容。它充满了各种注释和例子。如果它看起来让人害怕，请不要担心，我们马上就会修改它。

你同样可以在一个已经存在的目录下运行**vagrant init**去设置一个存在的项目。

Vagrantfile配置文件致力于对你的项目进行版本控制。如果你使用了版本控制，那么将Vagrantfilw纳入到版本控制中，这样每一个使用这个项目的人都可以直接使用而不需要做任何前期工作。

### 下一步

你已经成功的创建了你的第一个项目环境，请继续阅读,了解更多关于**Vagrant Boxes**。

---

## 容器(Boxes)

从头开始构建一个虚拟机，是单调乏味和效率低下的，相比之下 Vagrant 使用一个基础的镜像快速的克隆出一个虚拟机。这些基础的镜像在Vagrant被称为**容器(boxes)**,在你创建一个新的Vagrantfile配置文件之后你通常的一步是为你使用的Vagrant环境指定容器。

### 安装容器

如果你已经在开始页面运行了那些命令，那么你已经安装好了一个容器，同时不再需要在运行一次下面的命令。不管怎样，这一节都值得你继续阅读，了解更多关于如何管理容器。

将容器加入Vagrant使用 **vagrant box add** 命令。它给容器指定一个独有的名字，便于多个Vagrant环境可以复用它。如果你还没有添加一个容器，现在你可以这样做：

```shell
$ vagrant box add hashicorp/precise64
```

这条命令将从[HashiCorp's Atlas box catalog](https://atlas.hashicorp.com/boxes/search)下载一个名为“hashicorp/precise64"的容器，那里你可以发现和发布容器。这是你从那里下载容器最简单的方法，你同样可以通过本地文件，URL等方式来添加容器。

容器是为当前用户全局存储的，每一个项目使用的容器都是克隆过来的，不会对原镜像有任何修改。这样你就可以同时拥有两个都是使用我们刚才添加的**hashicorp/precise64**容器的项目。在任何一个项目中的操作都不会对另外一个有任何的影响。

通过上面的命令，你应该意识到容器是被命名的。命名分为两部分：用户名和容器名，使用一个斜杠分隔。在上面的例子中，用户名是"hashicorp",容器名是"precise64"。你同样可以使用URL或者本地文件的路径指定，但是这不在这个开始指导中。

>**命名空间并不保证是官方的容器！**一个通常的错误观念是一个命名空间像"ubuntu"代表着canonical的Ubuntu 容器。这是错误的，命名空间的查找行为跟Github的命名空间非常的相似，比如说，正如Github的支持团队无法协助某个人的仓库一样，HashiCorp的支持团队也无法协助第三方的容器。

### 使用容器

现在容器已经被加入Vagrant，我们需要配置我们的项目才能作为我们的基础环境。打开**Vagrantfile**配置文件，并加入下列改变：

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
end
```

容器名"hashicorp/precise64"必须和你前面添加进的容器名称相同。根据这个名字Vagrant才知道使用哪个容器。如果这个名字不是之前添加的，Vagrant将在运行时，自动下载并添加该容器。

你可以通过指定**config.vm.box_version**来指定容器的具体的版本，比如

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.box_version = "1.1.0"
end
```

你也可以直接使用**config.vm.box_url**指定容器的下载路径：

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"
end
```

在下一节，我们将启动Vagrant 虚拟机，同时交互一下。

### 查找更多的容器

在剩下的入门引导中，我们只使用我们之前添加"hashicorp/precise64"容器，但是在完成入门指导以后，你可能有一个问题，哪里可以找到更多的容器？

 寻找更多容器的最好地方是[HashiCorp's Atlas box catalog](https://atlas.hashicorp.com/boxes/search)。这里的公共目录有各种可以免费使用并可以运行在各种平台的容器。并且可以很方便的搜索功能方便你找到你所需要的容器。

除此之外，HashiCorp's 可以存储你的私有容器，这样你就可以创建只属于你的组织的容器。

### 下一步

你已经成功的下载了你的第一个Vagrant 容器，并已经配置Vagrantfile文件以使用容器。请继续阅读，了解更多启动和通过SSH登录Vagrant 虚拟机。

---

## 启动和SSH

现在是时候启动你的第一个虚拟机了。运行以下命令：

```shell
$ vagrant up
```

大概一分钟不到，这个命令将完成，并运行着一个Ubuntu的虚拟机。因为虚拟机并没有UI界面，所以你并不能真正的看到它。为了证明它已经运行，你可以使用SSH登陆它：

```shell
$ vagrant ssh
```

这条命令将打开一个完整的SSH会话，继续和虚拟机交互，你可以做任何你想做的操作，虽然虚拟机是临时的，但是小心**rm -rf /**命令，它将删除所有的文件，因为通过Vagrantfile配置文件，宿主机上配置的目录与虚拟机的/vagrant路径是共享的，这些文件也将被删除。在下一节，将介绍共享文件夹。

花一点时间思考下为什么会这样：只用了一行配置和一个命令，我们就启动了一个有完整的，SSH可以访问的虚拟机，太酷了。SSH会话可以通过**CTRL-D**快捷键结束。

```
vagrant@precise64:~$ logout
Connection to 127.0.0.1 closed.
```

当你摆弄完虚拟机，运行**vagrant destroy**，它将关闭这台虚拟机并删除这台虚拟机全部资源。

>**vagrant destroy**命令不会删除已经下载的容器。如果你需要删除它，你可以使用**vagrant box remove** 命令实现。

### 下一步

你已经成功的创建你的第一个虚拟机，并简单交互了一下。请继续阅读，了解更多关于同步目录。

---

# 命令行接口



---

# Vagrant 共享





---

# Vagrantfile 配置文件





---

# 容器(BOXES)

## 创建一个基础容器(box)

基础容器(base box)作为一个被人熟知的特别的一类，它们只包括最基本的Vagrant功能，它们不是由现存的Vagrant 环境重新打包制作的，这就是被称为基础(base)的原因。

例如，Vagrant 项目组提供的Ubuntu的基础容器。它们是从Ubuntu ISO 的最小安装方式创建的，而不是现有环境的重新打包。

建立一个干净的Vagrant 基础容器，对构建未来的开发环境是非常有用的。Vagrant 项目组希望在将来能够提供更多系统的基础容器。而现在，这页文档将指导你如何创建你自己的基础容器。

>高级主题！ 创建基础容器是漫长而且乏味的过程，因此不推荐给新的Vagrant使用者。如果你是Vagrant的新手，我们推荐你先使用现存的基础容器。

### 基础容器里面有什么？

基础容器通常只包括最低限度的的Vagrant功能软件集合。比如说，一个Linux容器可能只包括下面几个：

- 软件包管理。
- SSH
- SSH 用户，这样Vagrant才可以连接。
- 可能有 Chef，Puppet等，但不是必须的。

除了这个，每一个虚拟机管理工具可能需要额外的软件，比如，你使用VirtualBox制作一个基础容器，它需要安装Virtual guest additions，这样你才可以使用共享目录的功能。但是，如果你使用AWS基础容器，就不需要。

### 创建一个基础容器

创建一个基础容器是与虚拟机管理工具有关的，意味着使用VirtualBox，VMware，AWS等等的过程都是不同的，因此，这个文档不是一个创建基础容器的完全指导。

这一页将指导一个创建基础容器的共通之处，但无论如何，也会提供特定的虚拟机管理工具的指导链接。

特定的虚拟机管理工具的指导链接如下：

- [Docker Base Boxes](https://www.vagrantup.com/docs/docker/boxes.html)
- [Hyper-V Base Boxes](https://www.vagrantup.com/docs/hyperv/boxes.html)
- [VMware Base Boxes](https://www.vagrantup.com/docs/vmware/boxes.html)
- [VirtualBox Base Boxes](https://www.vagrantup.com/docs/virtualbox/boxes.html)

### Packer 和Atlas 工具

我们强烈推荐使用[Packer](https://www.packer.io/)来可重复的创建你的基础容器，它同时也是Atlas的自动化创建工具。阅读更多在Atlas的文档以了解[如何使用Packer创建Vagrant容器](https://atlas.hashicorp.com/help/packer/artifacts/creating-vagrant-boxes)。

### 磁盘空间

当你创建基础容器，应该确保分配足够的磁盘空间去保证用户可以正常使用。比如，在VirtualBox中，你应该给动态扩展的磁盘分配一个足够大的容量。给最终的使用者提供足够的灵活性。

如果你创建一个AWS基础容器，不要强行使用AMI分配TB大小的EBS存储。比如，当用户可以这样做以后，但是你应该默认安装临时的驱动，因为他们是免费而且提供大量的磁盘空间。

### 内存

像磁盘空间一样，找到一个合适的内存分配的平衡点是重要的。大多数的虚拟机管理软件，用户可以使用Vagrantfile配置使用的内存大小。所以不要默认的分配太多。如果**vagrant up**使用的时候需要数GB的内存，那么将会是糟糕的用户体验(令人震惊的)。相反，选择一个较低的值，比如512MB，它足够vagrant运行，但是在我们需要的时候也容易扩大它。

### 外围设备(声卡，USB等)

在基础容器中关闭这些并不是很必须的硬件，比如声卡和USB控制器。这些对于Vagrant用户来说通常是不需要的，而且他们在大多数情况下也可以很容易的在Vagrantfile中配置添加。

### 用户默认设置

Vagrant的几乎所有方面都可以修改。然而，Vagrant期望一些默认的配置，这些默认配置是你基础容器运行所需要的，如果你希望公开发行你的容器，你应该创建这些默认的设置。

如果你是为了私人使用而创建基础容器，你就不要在尝试下面这些了，因为它们会让你的基础容器暴露在安全风险之下。(可知的用户名，密码，密钥等等。)。

#### "vagrant" 用户

默认情况下，Vagrant希望使用"vagrant"用户通过SSH登录虚拟机。这个用户应该使用[不安全的密钥对](https://github.com/mitchellh/vagrant/tree/master/keys),这样Vagrant就可以默认使用SSH登录。同时，虽然Vagrant默认使用密钥对作为认证方式，依然有通过将"vagrant"用户的密码设置为"vagrant"来使用普通的方式登录，这样如果用户需要，他们可以手动登录。

为了配置SSH的不安全密钥对，将密钥的公钥写入"vagrant"用户的**~/.ssh/authorized_keys**文件。注意OpenSSH有着严格的权限机制。因此，你需要确保**~/.ssh**的权限是0700，而authorized_keys文件的权限是0600。

当Vagrant启动容器的时候将查找这个不安全的密钥对，它将自动使用一个随机生成的密钥对替换它，以保障它在运行时的安全。

#### Root 密码："vagrant"

Vagrant 并不希望并使用任何root密码。无论如何，使用一个统一的容易记忆的root密码可以让公众在需要的时候，更加方便的修改。

#### 无密码的Sudo

这是**十分重要**的。Vagrant的很多考虑都希望默认的用户可以使用无密码的**sudo**配置。这样可以方便Vagrant 配置网络，挂载同步目录，安装软件以及更多。

很多操作系统的最小安装并不会默认包含**sudo**程序，因此，你可能需要通过其他的方法安装sudo。

安装sudo程序以后，你需要配置它(一般使用**visudo**)而允许"vagrant"用户可以无密码的使用sudo。通过在配置文件的最后添加下面一行可以达到目的

```
vagrant ALL=(ALL) NOPASSWD: ALL
```

除外，Vagrant 并在通过SSH连接的时候不默认使用pty或者tty。你需要确保在sudo的配置文件没有**requiretty**在里面，如果有的话，删除它，他可以让sudo可以在没有tty的时候正确的运行。记住你可以通过配置Vagrant来让它可以支持pty，pty可以让你保存这个配置，但是Vagrant默认并不这样做。

#### SSH 优化

为了在使用的时保证SSH保持高速，同时不让Vagrant虚拟机连接到网络。需要将SSH服务的配置中的UseDNS设置为no。

这样可以避免因为连接的时候查询DNS而浪费几秒钟。

### Windows 容器

支持的Windows操作系统有:

- Windows 7
- Windows 8
- Windows Server 2008
- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2

Windows Server 2003 和Windows XP 是不被支持的，但是如果你是XP的死忠，[这里](https://stackoverflow.com/a/18593425/18475)可能能帮到你。

#### 基本的Windows 配置

- 关闭UAC
- 关闭复杂密码
- 关闭 "Shutdown Tracker"
- 在登录时关闭 "Server Manager"()

除了关闭UAC在控制面板，你同样需要在注册表中关闭它。不同的版本可以不同，但是Windows8/8.1使用下面的命令。它可以允许一些操作，比如自动Puppet安装Vagrant的Windows基础容器。

```
reg add HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\System /v EnableLUA /d 0 /t REG_DWORD /f /reg:64
```

#### 基本的WinRM 配置

为了打开并配置WinRM，你需要将WinRM服务设置为自动开始和允许未加密的基础认证(很显然这是不安全的)。在Windows的命令窗口运行以下的指令：

```
winrm quickconfig -q
winrm set winrm/config/winrs @{MaxMemoryPerShellMB="512"}
winrm set winrm/config @{MaxTimeoutms="1800000"}
winrm set winrm/config/service @{AllowUnencrypted="true"}
winrm set winrm/config/service/auth @{Basic="true"}
sc config WinRM start= auto
```

#### 附加的WinRM 1.1 配置

这些额外的配置是专门为Windows Server 2008(WinRM 1.1)特定的。对于Windows Server 2008 R2, Windows 7 以及更新的Windows版本，你可以忽略这一小节。

1. 确认Windows PowerShell 功能以及安装。
2. 将WinRM的端口号改为5985或者升级为WinRM 2.0

下面的命令可以将WinRM的端口号修改为Vagrant所需要的：

```
netsh firewall add portopening TCP 5985 "Port 5985"
winrm set winrm/config/listener?Address=*+Transport=HTTP @{Port="5985"}
```

### 其它的软件

现在，你已经安装了所有你的基础容器可以和vagrant一起使用所需要的软件。然而，如果你愿意，这里有一些额外的软件可以安装。

我们计划在将来，Vagrant在使用那些虚拟机管理器时，依旧不自动安装Chef或者Puppet。用户可以使用一个Shell来安装，但是，如果你你想在容器以外使用Chef/Puppet,你将需要在基础容器中安装它们。

安装它们已经超过了本页的内容，但是应该是十分的简单。

此外，随意安装软件和配置你想要的其他软件，会让你想要将它们在基础容器添加为默认的。

### 打包容器

将容器打包成容器文件依赖于具体的虚拟机管理器。请查看具体的虚拟机管理器的文档的相关内容。一些虚拟机管理器的文档链接在本页的开始部分。

### 发布这个容器

如果你愿意，你可以发布这个容器文件。而如果你希望它支持版本，通过单个URL得到不同虚拟机管理器的版本，发布更新，分析，等功能。我们建议你将它加入到[HashiCorp's Atlas](https://www.vagrantup.com/docs/other/atlas.html)。

你还可以在其上上传公共和私有的容器。

### 测试这个容器

假如你是Vagrant的新手，给你一个大概的命令：

```
$ vagrant box add my-box /path/to/the/new.box
...
$ vagrant init my-box
...
$ vagrant up
...
```

如果你使用其他的虚拟机管理器，在**vagrant up**使用**—provider** 参数指定使用的管理器，如果允许成功，你的容器可用。

---

# 发布







---

# 网络



---

# 同步目录



---

# 多台虚拟机



---

# 虚拟机管理器(providers)

---

# 插件



---


















