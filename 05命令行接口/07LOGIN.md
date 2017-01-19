# LOGIN

命令：**vagrant login**

这条登录命令用来为[HashiCorp's Atlas](https://www.vagrantup.com/docs/other/atlas.html)的服务进行认证。只有当你需要使用受限制访问的容器或者使用**Vagrant Share**时才有必要登录。

**不需要登录也可以正常使用Vagrant**。Vagrant的大量主要功能都不需要登录。只有确定的功能比如：访问受限制的容器或者**Vagrant Share**才需要登录。

这条命令可用的标志在下面：

## 选项

- **—check** - 检查你是否已经登录。输出你是否已经登录。如果你已经登录，运行结果就返回0，如果没有则返回1。
- **—logout** -  如果你已经登录，那么你将登出。如果你已经登出，那么将什么也不做。所以在你登出以后运行这么命令不会发生错误。
- **—token** - 使用给定的字符串作为Altas登录的认证密钥。

## 示例

使用用户和密码安全登录Atlas：

``` shell
$ vagrant login
# ...
Atlas username:
Atlas password:
```

检查当前用户是否已经登录：

``` shell
$ vagrant login --check
You are already logged in.
```

使用认证密钥登录：

``` shell
$ vagrant login --token ABCD1234
The token was successfully saved.
```



