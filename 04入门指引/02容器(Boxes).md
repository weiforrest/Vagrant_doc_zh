# 容器(Boxes)

从头开始构建一个虚拟机，是单调乏味和效率低下的，相比之下 Vagrant 使用一个基础的镜像快速的克隆出一个虚拟机。这些基础的镜像在Vagrant被称为**容器(boxes)**,在你创建一个新的Vagrantfile配置文件之后你通常的一步是为你使用的Vagrant环境指定容器。

## 安装容器

如果你已经在开始页面运行了那些命令，那么你已经安装好了一个容器，同时不再需要在运行一次下面的命令。不管怎样，这一节都值得你继续阅读，了解更多关于如何管理容器。

将容器加入Vagrant使用 **vagrant box add** 命令。它给容器指定一个独有的名字，便于多个Vagrant环境可以复用它。如果你还没有添加一个容器，现在你可以这样做：

```shell
$ vagrant box add hashicorp/precise64
```

这条命令将从[HashiCorp's Atlas box catalog](https://atlas.hashicorp.com/boxes/search)下载一个名为“hashicorp/precise64"的容器，那里你可以发现和发布容器。这是你从那里下载容器最简单的方法，你同样可以通过本地文件，URL等方式来添加容器。

容器是为当前用户全局存储的，每一个项目使用的容器都是克隆过来的，不会对原镜像有任何修改。这样你就可以同时拥有两个都是使用我们刚才添加的**hashicorp/precise64**容器的项目。在任何一个项目中的操作都不会对另外一个有任何的影响。

通过上面的命令，你应该意识到容器是被命名的。命名分为两部分：用户名和容器名，使用一个斜杠分隔。在上面的例子中，用户名是"hashicorp",容器名是"precise64"。你同样可以使用URL或者本地文件的路径指定，但是这不在这个开始指导中。

> **命名空间并不保证是官方的容器！**一个通常的错误观念是一个命名空间像"ubuntu"代表着canonical的Ubuntu 容器。这是错误的，命名空间的查找行为跟Github的命名空间非常的相似，比如说，正如Github的支持团队无法协助某个人的仓库一样，HashiCorp的支持团队也无法协助第三方的容器。

## 使用容器

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

## 查找更多的容器

在剩下的入门引导中，我们只使用我们之前添加"hashicorp/precise64"容器，但是在完成入门指导以后，你可能有一个问题，哪里可以找到更多的容器？

 寻找更多容器的最好地方是[HashiCorp's Atlas box catalog](https://atlas.hashicorp.com/boxes/search)。这里的公共目录有各种可以免费使用并可以运行在各种平台的容器。并且可以很方便的搜索功能方便你找到你所需要的容器。

除此之外，HashiCorp's 可以存储你的私有容器，这样你就可以创建只属于你的组织的容器。

##下一步

你已经成功的下载了你的第一个Vagrant 容器，并已经配置Vagrantfile文件以使用容器。请继续阅读，了解更多启动和通过SSH登录Vagrant 虚拟机。