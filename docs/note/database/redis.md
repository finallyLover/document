# redis

## redis安装(普通安装)

### redis下载

`https://redis.io/download/`

### redis 复制到服务器

### redis解压

`tar -xzvf redis-6.2.6.tar.gz`

### 修改配置文件（redis.conf）

根据实际情况修改

### 进入redis根目录 安装redis

`make install PREFIX=/usr/local/redis`

### 将配置文件文件复制到安装目录下

### 启动

`./redis-server redis.conf`

### 登录

`./redis-cli -p 端口号 -a 密码`

`./redis-cli -p 6380 -a 123456`





## redis 常规配置

### 
