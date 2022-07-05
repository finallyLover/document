# NFS共享文件搭建

客户端（81.68.183.233） 、服务端（1.116.22.15）

## NFS 

### 检查是否安装

`rpm -qa|grep nfs`

`rpm -qa|grep rpc`

### 安装

`yum install -y rpcbind`

`yum install -y nfs-utils`

### 启动

`sudo service rpcbind start`

`sudo service nfs start`

### 设置开机启动

`chkconfig rpcbind on`

`chkconfig nfs on`

### 查看启动状态

` sudo service rpcbind status`

` sudo service nfs status`

### 停止服务

` sudo service rpcbind stop`

` sudo service nfs stop`

## 配置

### 服务端配置

```
vim /etc/exports 

/nfs 1.116.22.15(rw,no_root_squash,no_all_squash,sync)
备注：
    /nfs 为可以共享的文件路径
     1.116.22.15 客户端地址   
     
配置完成后重启服务 
```

### 客户端配置

```
mount -t nfs 1.116.22.15:/nfs /nfs
```

 服务端会与客户端数据一致性