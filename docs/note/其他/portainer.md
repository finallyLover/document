# portainer

## 安装（docker）

```sell
docker run -d -p 9000:9000 \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
--name prtainer \
docker.io/portainer/portainer

```

