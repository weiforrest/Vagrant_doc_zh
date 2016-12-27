# BOX

---

命令：**vagrant box**

这个命令是用来管理(添加，删除等)容器。

这个命令的主要的功能通过以下子命令完成：

- **add**
- **list**
- **outdated**
- **remove**
- **repackage**
- **update**

# BOX ADD

---

命令：**vagrant box add ADDRESS**

通过给定的容器地址，将容器添加到Vagrant中。这个地址可以死以下三类：

- [Vagrant 可用镜像的简称](https://atlas.hashicorp.com/boxes/search)，比如"hashicorp/precise64"。
- [目录](https://atlas.hashicorp.com/boxes/search)中容器的文件路径或者HTTP URL。如果是HTTP，支持普通认证，需要制定[http_proxy](https://www.vagrantup.com/docs/cli/box.html#http_proxy)环境变量。HTTPS同样被支持。
- 容器文件的直接路径。这种情况，你必须使用**--name**标志(见后续)，同时versioning/updates 都不能使用。

如果在下载过程中发生错误或者通过Ctrl-C 中断，Vagrant会在下一次请求的时候尝试恢复下载。但是只能恢复24小时以内的。

## 选项

- **--box-version VALUE** - 指定你想添加容器的版本。默认为添加最新的版本。版本的值可以是准确的版本号，比如"1.2.3"或者是一个版本限制，比如：">=1.0, < 2.0"。
- **--cacert CERTFILE** -  指定用于CA验证的证书。如果远端没有使用标准的根证书，则需要指定该选项。
- **--capath CERTDIR** -   指定用于CA验证的证书目录。如果远端没有使用标准的根证书，则需要指定该选项。
- **--cert CERTFILE** - 下载容器时使用的客户证书，如果需要的话。
- **--clean** - 当被指定，Vagrant将删除所有通过相同URL下载的旧的临时文件，可能因为内容已经变了，而你不想Vagrant继续之前的下载，这将是非常有用的。
- **--force** 当被指定，容器将被下载并强制覆盖现有的文件。
- **--insecure** - 当被指定，当使用HTTP URL时，将不进行SSL认证。
- **--provider PROVIDER** -当被指定，Vagrant将确认容器为你指定的管理器，默认情况下，Vagrant自动检测并使用合适的管理器。

## 本地容器选项

这些选项只能应用在你自己添加本地容器时(没有使用容器目录)。

- **--checksum VALUE** - 下载时容器的校验值。如果被指定，Vagrant将比较实际下载的校验值和给定的校验值，以匹配是否有错误发生。在容器文件十分大的时候，高度推荐使用。同时**--checksum-type** 也需要被指定。如果你通过目录下载容器，目录内已经包含了校验值。
- **--checksum-type TYPE** - 指定**--checksum**时使用的校验值得类型，当前支持的类型有"md5","sha1"和"sha256"。
- **--name VALUE** - 容器的名称，这个值是你准备放在Vagrantfile中**config.vm.box**的值。当你通过目录下载容器时，它已经包含在目录中，不需要额外的指定。

> **HashiCorp's Atlas 上的容器的容器版本校验值**:HashiCorp's Atlas的容器，它们的校验值都已经嵌入在了容器的元数据当中，而元数据在TLS层上，并且它们的格式也是验证过的。

# BOX LIST

---

命令：**vagrant box list**

这条命令列出所有你已经安装在Vagrant中的容器。

# BOX OUTDATED

---

命令： **vagrant box outdated**

这条命令将告诉你当前你在Vagrant环境中使用的容器是不是已经过期。如果指定**--global**标志，将检查你所有已安装的容器。

检查更新是通过刷新容器相关的元数据，这通常需要网络连接。

## 选项

- **--global** - 检查所有已安装容器的更新，而不只是当前Vagrant环境中的容器。

# BOX REMOVE

---

命令：**vagrant box remove NAME**

这条命令将从vagrant中删除给定名字的容器。

如果容器有多个管理器，可以通过指定**--provider**标志来指定管理器。如果容器有多个版本，可以通过**--box-version** 来指定想要删除的版本或者通过**--all** 标志删除所有的版本。

## 选项

- **--box-version VALUE** - 想要删除容器的版本，这个标志的更多细节请看**box add**。
- **--all** - 删除容器所有可用的版本。
- **--force** - 强制删除容器，无论Vagrant环境是否在使用。
- **--provider VALUE** - 删除指定管理器的容器，只有在容器包含多个管理器的情况下使用。如果只有一个管理器，Vagrant可以默认的删除它。

# BOX PRUNE

---

命令：**vagrant box prune**

这天命令将删除所有已经安装容器的旧的版本。如果容器正在使用，Vagrant将向你确认。

## 选项

- **--provider PROVIDER** 指定容器使用的管理器。
- **--dry-run** - 只输出将要被删除的容器。
- **--name NAME** - 指定需要检查更新版本的容器名称。
- **--force** - 无论容器是否被使用，强制删除。

# BOX REPACKAGE

---

命令：**vagrant box repackage NAME PROVIDER VERSION**

这个命令将重新打包指定的容器，将其放在当前的目录，这样你可以重新发布它。名称，管理器，版本可以通过**vagrant box list** 获取。

当你添加一个容器时，Vagrant将解压它并存储它，原始的**.box**文件不在需要。这条命令可以很好的从一个已经安装的容器中恢复**.box**文件。

# BOX UPDATE

---

命令： **vagrant box update**

这条命令将在当前环境中的容器有更新时，更新它。这条命令也可以通过**--box**指定需要更新的容器(在当前Vagrant环境之外)。

需要注意的是如果当前容器正在运行，将不会更新容器。需要销毁当前的容器并重新建立它。

如果你只是想查看那些更新可以，使用**vagrant box outdated**命令。

## 选项

- **--box VALUE** - 指定需要更新的容器，如果这个标志没有被指定，Vagrant将更新当前环境中的容器。
- **--provider VALUE** - 当**--box** 被指定时，这个可以指定特定管理器的容器，如果没有使用多个管理器，该标志不需要。必须和**--box**标志一起使用。






