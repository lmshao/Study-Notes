#1. NFS
##Ubuntu  

Install
```sh
$ sudo apt-get install nfs-kernel-server
```

Configure

```sh
$ sudo sed -i '$a /nfs    192.168.1.*(rw,sync,no_root_squash,no_subtree_check)' /etc/exports
```

Start
```
$ sudo service portmap start
$ sudo service nfs-kernel-server start
```

Mount
```sh
$ mount -t nfs 192.168.1.100:/nfs /mnt
```

#2. SSH
## Ubuntu
Install   
```
​$sudo apt-get install openssh-server
```

​2. 开启SSH服务

​​$sudo service ssh start    或    $sudo /etc/init.d/ssh start

​3.​ 查看SSH服务状态

​​$sudo service ssh status    或    $sudo initctl list | grep ssh

4. 常用命令

​$sudo service ssh stop （关闭）

​​$sudo service ssh restart （重启）