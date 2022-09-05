# Git



## 安装（git）

```
#安装
yum install git
#查看版本 git --version
```



## git中克隆

```
git clone  http://用户名:密码@地址
备注 用户名或者密码中有@符号 需要转义  @ 为%40
git clone  http://cuisiyu:1qaz%40WSX@work.micolor.net:5030/gitblit/r/housekeeping-mobile-worker.git


```

## git查看克隆路径

```
git remote -v
```

![image-20220620134936250](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220620134936250.png)

## git中导出csv日志记录

```sell
bash 中
#导入
git log --date=iso --pretty=format:'"%h","%an","%ad","%s"' >log.csv
备注： 如果出现乱码设置 如果gbk 不行就utf-8
 git config --global i18n.commitencoding gbk
 git config --global i18n.logoutputencoding gbk
 export LESSCHARSET=gbk
```

