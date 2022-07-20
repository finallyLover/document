# docker 
## 常用命令
### docker 容器与本地文件互相拷贝

Docker容器中的文件拷贝至本地
```
#格式
#docker cp CONTAINER ID:容器目录 本地目录
#示例
docker ps -a  #查看本地容器ID 
sudo docker cp 52ea915e6527:/aha /home/aha2
```
本地文件拷贝至容器
```
#格式
#docker cp 本地路径 CONTAINER ID:容器目录
#示例
docker cp license.dat 52ea915e6527:/home
```

==备注：此命令是在容器外使用(shell或cmd)==