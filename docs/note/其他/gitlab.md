# gitlib 

## 安装（docker）

```sell
# 查找Gitlab镜像
docker search gitlab

# 拉取Gitlab镜像
docker pull gitlab/gitlab-ce:latest

# 启动容器
docker run \
 -itd  \
 -p 9980:9980 \
 -p 9922:9922 \
 -v /home/gitlab/etc:/etc/gitlab  \
 -v /home/gitlab/log:/var/log/gitlab \
 -v /home/gitlab/opt:/var/opt/gitlab \
 --restart always \
 --privileged=true \
 --name gitlab \
 gitlab/gitlab-ce
```

