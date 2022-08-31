# liunx常用命令

## 用户命令

### 创建用户

`useradd 用户名`

### 添加密码(密码会输入两次)

`passwd 密码`

### 授权用户文件

`chown -R 用户名称 路径`

例如：==chown es /mydata/elasticsearch-8.1.2==

### 更改文件权限

`chmod  权限数字 文件名称`

例如：==chmod 777 elasticsearch-8.1.2==

### 切换用户

`su 用户名`



## 查找命令

### 查询文件夹

`find / -name "文件名"`

例如：`find / -name "elasticsearch"`



## 复制命令

cp [选项] 源文件 目标文件

`cp redis.conf /mydata/redis-s/bin`

![image-20220429142449273](https://gitee.com/finallylover/imgupload/raw/master/img/image-20220429142449273.png)

## 远程操作其他服务器命令

### 安装sshpass （两种安装方式）

1. sudo apt-get install sshpass

2. yum install sshpass

   备注:使用前需要登录服务器地址
   
   `ssh 用户名@地址`
   
   ```shell
   #文件复制
   sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' scp -P 22 ruoyi-admin.jar ubuntu@175.178.85.9:/home/jyz/app/ruoyi-admin.jar
   #普通命令
   sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 " rm  /home/jyz/app/sys-error.log"
   
   ```
   
   

## 杀死进程命令

###  安装

 sudo apt-get install killall

killall 进程名称

### 查询进程并且杀死

```shell
ps -aux|grep ruoyi-wechat|grep -v grep|awk '{print $2}'|xargs -r kill -9

备注 解释
	ps -aux|grep ruoyi-wechat 查询进程信息
	grep -v grep 显示不包含匹配文本的所有行，在这里为筛选出所有不包含grep名称的进程，对上一步的进程再做一次筛选
	awk 在文件或字符串中基于指定规则浏览和抽取信息，把文件逐行读入，以空格为默认分隔符将每行切片，然后进行后续处理。这里利用awk '{print $2}' 将上一步中过滤得到的进程进行打印，$2表示打印第二个域（PID, 进程号） $0 表示所有域，$1表示第一个域，$n表示第n个域
	xargs 命令是给命令传递参数的过滤器，善于把标准数据转换成命令行参数。在这里则是获取前一个命令的输出，把它转换成命令行参数传递给后面的kill命令。-r选项表示如果输入为空，则不执行后面的命令
	kill -9 强制关闭进程
```

## 定义变量 使用变量

备注：1、不能已数字开头 

​			2、区分大小写

​			3、不能以数字开头

​			4、等号两边不能有空格

​			5、可以使用``包裹进行引用

![image-20220520170739366](https://gitee.com/finallylover/imgupload/raw/master/img/image-20220520170739366.png)

```shell
adminpid=`sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 "sudo ps -aux|grep ruoyi-admin|grep -v grep"|awk '{print $2}'|xargs`
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 "kill -9 `echo ${adminpid}`"
```

