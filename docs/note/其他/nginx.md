# nginx

## liunx 安装

```sell
#下载
 wget -c https://nginx.org/download/nginx-1.12.0.tar.gz
#解压
tar -zxvf nginx-1.12.0.tar.gz
# 进入目录
cd nginx-1.12.0

#安装其他依赖
yum install pcre-devel zlib zlib-devel openssl openssl-devel
#安装编译器
yum install gcc -y

指定编译
CC=gcc
export CC
#配置
./configure
安装
make && make install
#查找安装目录
whereis nginx
# 进入安装目录
cd /usr/local/nginx/sbin/

# 启动命令 在/usr/local/nginx/sbin目录下执行
./nginx

# 关闭命令 在/usr/local/nginx/sbin目录下执行
./nginx -s stop

# 重新加载命令 在/usr/local/nginx/sbin目录下执行
./nginx -s reload
```

