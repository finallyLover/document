下载

 wget https://archive.apache.org/dist/kafka/3.1.0/kafka_2.12-3.1.0.tgz



windows 下启动kafka

根部目录下

```
先启动zookeeper,默认自带的
bin\windows\zookeeper-server-start.bat config\zookeeper.properties
然后启动kafka服务
bin\windows\kafka-server-start.bat .\config\server.properties

bin\windows\kafka-topics.b --list --bootstrap-server localhost:9092
```







```
先启动zookeeper,默认自带的
bin/zookeeper-server-start.sh config/zookeeper.properties
然后启动kafka服务
bin/kafka-server-start.sh config/server.properties
列举拥有哪些topics
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
```

### 错误（err）

#### java.net.UnknownHostException: VM-4-12-centos

解决方案（/house/kafka/kafka_2.12-3.1.0/config/server.properties）

​	将localhost 改为127.0.0.1 则可以解决

![img](kafka.assets/NEKN0$[$I3Q`B]`2SA9ZHR5.png)