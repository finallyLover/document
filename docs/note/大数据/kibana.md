# kibana 开源可视化分析工具

## 安装（普通方式）

### 下载 
`wget https://artifacts.elastic.co/downloads/kibana/kibana-7.6.0-linux-x86_64.tar.gz`

### 解压
 `tar -xzvf kibana-7.6.0-linux-x86_64.tar.gz `

## 安装（docker）
### 拉取
`docker pull kibana:7.6.0`

### 启动
`docker run --name kibana -e ELASTICSEARCH_HOSTS=http://自己的elasticsearchIP地址:9200 -p 5601:5601 -d kibana:7.6.0`



## 设置中文显示

 /config/kibana.yml 

添加 `i18n.locale: "zh-CN"`