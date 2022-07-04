# node

## node安装 （liunx）

### 下载安装包

`wget https://nodejs.org/dist/v14.15.4/node-v14.15.4-linux-x64.tar.xz`

### 解压

`tar -xf node-v14.15.4-linux-x64.tar.xz`

### 建立软连接

```sell
cd /usr/bin

in -s 解压文件目录 名称
ln -s /usr/local/node/bin/node node
ln -s /usr/local/node/bin/npm npm
```

### 查看版本

`node -v`  `npm -v`