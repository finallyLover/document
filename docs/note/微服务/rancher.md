# rancher

## docker 安装

```
# 拉取
docker pull rancher/rancher:v2.5.12
# 创建
mkdir -p /mount/rancher/rancher
mkdir -p /mount/rancher/log
mkdir -p /mount/rancher/kubelet
mkdir -p /mount/rancher/cni

#启动
docker run --privileged -d --restart=unless-stopped -p 81:80 -p 444:443 \
-v /mount/rancher/rancher:/var/lib/rancher \
-v /mount/rancher/log:/var/log \
-v /mount/rancher/cni:/var/lib/cni \
-v /mount/rancher/kubelet:/var/lib/kubelet \
--name rancher rancher/rancher:v2.5.12
```

## 访问

ip地址:444
