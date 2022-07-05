# jdk

## jdk（yum安装）

### 下载

`yum install -y java-1.8.0-openjdk.x86_64`

### 安装路径（默认安装路径）

`usr/lib/jvm`

### 查看版本号

`java -version`

## jdk（普通安装）

### 下载

https://www.oracle.com/java/technologies/downloads/#java8



` wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u141-b15/336fa29ff2bb4ef291e347e091f7f4a7/jdk-8u141-linux-x64.tar.gz"`

### 将文件复制到服务器



### 解压文件

`tar -xzvf jdk-8u321-linux-i586.tar.gz `

### 配置环境变量

`vim /etc/profile`

添加如下配置

```
export JAVA_HOME=/mydata/jdk8/jdk1.8.0_321 ##解压实际路径
export CLASSPATH=.:$JAVA_HOME/lib:$CLASSPATH
export PATH=$PATH:$JAVA_HOME/bin
```

### 刷新环境变量

`source /etc/profile`

### 查看版本

`java -version`

### 备注

如果安装配置后报“bad ELF interpreter: 没有那个文件或目录”的错误

请安装 glibc

`yum -y install glibc.i686`

