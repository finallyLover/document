# skywalking 链路追踪

## 安装（docker）

```

# 服务端
docker run \
--name skywalking-oap \
--restart always \
-p 11800:11800 \
-p 12800:12800 -d \
--privileged=true \
-e TZ=Asia/Shanghai \
-e SW_STORAGE=elasticsearch7 \
-e SW_STORAGE_ES_CLUSTER_NODES=192.168.0.100:9200 \
-v /etc/localtime:/etc/localtime:ro \
apache/skywalking-oap-server:8.6.0-es7


# ui 界面
docker run \
--name skywalking-ui \
--restart always \
-p 8081:8080 -d \
--privileged=true \
--link skywalking-oap:skywalking-oap \
-e TZ=Asia/Shanghai \
-e SW_OAP_ADDRESS=192.168.0.100:128 \
-v /etc/localtime:/etc/localtime:ro \
apache/skywalking-ui:8.6.0

```

