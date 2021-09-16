# Debian系统初始化要做的事


## 1.修改root密码

```
$ passwd root
```

查看IP地址
```
$ ip address
```

## 2.安装防火墙

```
$ apt-get install ufw #安装
$ ufw status #查看现有规则
$ ufw enable
$ ufw disable
$ ufw allow 22/tcp
$ ufw allow 80
$ ufw delete allow 80
$ ufw allow from xx.xx.xx.xx to any port 22 #指定ip访问端口
```

## 3.修改默认ssh端口

端口都搞定之后，接下来就是修改ssh配置文件。
```
$ vi /etc/ssh/sshd_config
```
在 #Port 22 这一行下面 加入 Port 66 然后别忘了防火墙开放66端口(上面已经做过了)。

保存之后重启sshd服务
```
$ service sshd restart
```

## 4.修改时间

执行下面命令找到：Asia/Shanghai
```
$ timedatectl list-timezones
```

```
$ timedatectl set-timezone Asia/Shanghai
```

## 5.安装docker和docker-compose

```
$ curl -fsSL https://get.docker.com | bash -s docker
```

使用阿里云镜像
```
$ curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

或者国内源
```
$ curl -sSL https://get.daocloud.io/docker | sh
```

安装完docker之后，安装docker-compose
```
$ apt -y install docker-compose
```

## 6.解决vim不能复制的问题

很简单，只需要改动一个文件就可以啦！编辑文件/etc/vim/vimrc.local, 添加下面几行
```
source $VIMRUNTIME/defaults.vim
let skip_defaults_vim = 1
if has('mouse')
    set mouse=r
endif
```

