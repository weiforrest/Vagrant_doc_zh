# 部署(PROVISIONING)

现在，我们已经有了一个运行Ubuntu基本副本的虚拟机，我们可以在我们的宿主机中编辑文件，使用同步目录同步相应的更改到虚拟机中。现在让我们使用网络服务器发布它们。

我们可以使用SSH登录，然后安装一个网络服务器。那么所有使用Vagrant的人都需要执行同样的操作。相反，Vagrant内置支持自动部署，通过这个特性，Vagrant将在**vagrant up**时自动的安装软件，这样客户虚拟机可以被重复的创建，并且是现成可用的。

## 安装阿帕奇(APACHE)

我们将只为我们的基本工程安装[Apache](http://httpd.apache.org),我们可以通过使用一个shell脚本来完成。创建如下的shell脚本，并保存为**bootstrap.sh**在Vagrantfile所在的目录：

``` shell
#!/usr/bin/env bash

apt-get update
apt-get install -y apache2
if ! [ -L /var/www ]; then
  rm -rf /var/www
  ln -fs /vagrant /var/www
fi
```

接下来，我们配置Vagrant在设置虚拟机的时候运行这个脚本。编辑Vagrantfile文件，如下所示：

``` 
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.provision :shell, path: "bootstrap.sh"
end
```

"provision"这一行是新添加的，它将告诉Vagrant 使用**shell**部署器通过**bootstrap.sh**文件来设置虚拟机。文件路径是以项目根目录为基准路径。

## 部署！

在所有的一切都被部署好以后，只需要运行**vagrant up**来创建你的虚拟机，Vagrant将自动的部署好它。你可以在你的终端上看到shell脚本运行的输出。如果客户虚拟机通过之前的操作已经运行，那么运行**vagrant reload —provision**快速重启虚拟机，并跳过初始的导入步骤。通常Vagrant只在第一次使用**vagrant up**时，使用重载命令中的部署选项指导Vagrant运行部署器。

在Vagrant完成运行以后，网络服务器已经启动并运行。你无法通过你自己的浏览器来查看你，但是你可以通过SSH登录你的虚拟机确认配置文件是否生效：

``` shell
$ vagrant ssh
...
vagrant@precise64:~$ wget -qO- 127.0.0.1
```

这样做的原因是我们在脚本中安装了Apache，同时将Apache默认的**DocumentRoot**指向到我们的**/vagrant**目录，同时也是Vagrant默认使用的同步目录。

你可以创建更多的文件，并在终端上看到他们，但是在下面的操作将覆盖现有的网络配置，这样我们就可以在宿主机上通过浏览器访问虚拟机了。

> **更复杂的部署脚本**，它可能对打包使用预安装包定制的Vagrant容器更有效，以取代每次构建的麻烦，这个主题已经超过了入门指引，但可以在打包定制容器文档中找到。

## 下一步

你已经成功的使用Vagrant配置你的第一个虚拟机，请继续阅读了解更多关于[网络]()的内容。