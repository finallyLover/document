# EFK (Elasticsearch + Fluentd + Kibana)日志分析系统



```shell
 docker run -d -e ES_JAVA_POTS="-Xms256m -Xmx256m"  -e "discovery.type=single-node" -p 9200:9200 -p 9300:9300  --name elasticsearch elasticsearch:7.7.1


docker run --link elasticsearch:7.7.1 -p 5601:5601 -d  --name kibana kibana:7.7.1


docker  pull  willfarrell/filebeat 

docker run --restart=always --log-driver json-file --log-opt max-size=100m --log-opt max-file=2 \
--name filebeat --user=root -d \
-v /house/images/logs/:/logs/ \
-v /house/filebeat/filebeat.docker.yml:/etc/filebeat/filebeat.yml  willfarrell/filebeat:latest


下载
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.9.1-linux-x86_64.tar.gz
解压
tar -zxvf filebeat-7.9.1-linux-x86_64.tar.gz
启动
./filebeat -e -c filebeat.yml

```

