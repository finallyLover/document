# 安装

## docker 安装

```


docker run -d --name sonarqube -v /home/sonarqube/plugins:/extensions/plugins -v /home/sonarqube/config:/conf  -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9005:9000 sonarqube:latest
```

