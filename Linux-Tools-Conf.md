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