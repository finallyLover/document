# jenkins

## jenkins安装（docker）

### docker 拉取

`docker pull jenkins/jenkins`

### 创建挂载文件

`mkdir -p /var/jenkins_mount`

### 文件授权

`chmod 777 /var/jenkins_mount`

### 启动

​		-d 后台运行镜像

　　-p 10240:8080 将镜像的8080端口映射到服务器的10240端口。

　　-p 10241:50000 将镜像的50000端口映射到服务器的10241端口

　　-v /var/jenkins_mount:/var/jenkins_mount /var/jenkins_home目录为容器jenkins工作目录，我们将硬盘上的一个目录挂载到这个位置，方便后续更新镜像后继续使用原来的工作目录。这里我们设置的就是上面我们创建的 /var/jenkins_mount目录

　　-v /etc/localtime:/etc/localtime让容器使用和服务器同样的时间设置。

　　--name myjenkins 给容器起一个别名

`docker run -d -p 10240:8080 -p 10241:50000 -v /var/jenkins_mount:/var/jenkins_home -v /etc/localtime:/etc/localtime --name myjenkins jenkins/jenkins`

### 密码查看

`vi /var/jenkins_mount/secrets/initialAdminPassword`

## jenkins安装（常规安装）

### jdk安装

1. 官网下载：https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html

![image-20220411094910469](../images/20220411094910469.png)

2. 将文件复制到服务器中

3. 进入目录，jdk解压：`tar -xzvf jdk-8u202-linux-x64.tar.gz`

4. 编辑/etc/profile文件 添加如下配置

   ```
   export JAVA_HOME=/house/jdk1.8.0_202
   export CLASSPATH=.:$JAVA_HOME/lib:$CLASSPATH
   export PATH=$PATH:$JAVA_HOME/bin
   ```

   ### jenkins启动

```
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum install jenkins
查看文件
rpm -ql jenkins 找到war进行启动
启动 指定端口
 java -jar /usr/share/java/jenkins.war --ajp13Port=-1 --httpPort=10240
```

## jenkins使用

### 新建item

![image-20220704163845535](images/image-20220704163845535.png)

![image-20220704163845535](images/image-20220704163845535.png)

![image-20220411095542315](https://gitee.com/finallylover/imgupload/raw/master/img/image-20220411095542315.png)

### 添加淘汰策略

![image-20220411095625673](https://gitee.com/finallylover/imgupload/raw/master/img/image-20220411095625673.png)

### 添加shell脚本（docker 方式 后端）

![image-20220411095700711](https://gitee.com/finallylover/imgupload/raw/master/img/image-20220411095700711.png)

```shell
#!/bin/bash
params=(test 8080 prod)
cd /house/git_rep/${params[0]}
git pull origin master
export JAVA_HOME=/house/jdk1.8.0_202
/house/apache-maven-3.8.5/bin/mvn clean package -Dmaven.test.skip=true -P${params[2]} install 
docker rm -f ${params[0]}
docker rmi --force ${params[0]}:latest
cd /house/git_rep/${params[0]}/src/main/resources
docker build  -f /house/git_rep/${params[0]}/src/main/resources/dockerfile.${params[0]} -t ${params[0]}:latest --no-cache .
docker run -p ${params[1]}:${params[1]} --net "host" --name ${params[0]} -d  ${params[0]}:latest 
#docker container prune -f
```

### 添加shell 脚本（jar包方式 后端）

备注：sshpass 需要安装 

```shell
#!/bin/bash
params=(housekeeping-service-new 8080 prod)
cd /house/git_rep/${params[0]}/
git checkout main
git pull origin main
export JAVA_HOME=/opt/jdk-13/ 
/opt/apache-maven-3.8.4/bin/mvn clean package -P ${params[2]} -Dmaven.test.skip=true install 
cd /house/git_rep/${params[0]}/ruoyi-admin/target/
adminpid=`sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 "sudo ps -aux|grep ruoyi-admin|grep -v grep"|awk '{print $2}'|xargs`
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 "kill -9 `echo ${adminpid}`"
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 "mv /home/jyz/app/ruoyi-admin.jar /home/jyz/app/ruoyi-admin-$(date +%Y%m%d).bak"
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' scp -P 22 ruoyi-admin.jar ubuntu@175.178.85.9:/home/jyz/app/ruoyi-admin.jar
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 " rm  /home/jyz/app/logs/sys-error.log"
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 " rm  /home/jyz/app/logs/sys-info.log"
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 " rm  /home/jyz/app/logs/sys-user.log"
sshpass -p 'JkBrVKmMy3dcCdGb7T6b8C' ssh ubuntu@175.178.85.9 "nohup java -jar /home/jyz/app/ruoyi-admin.jar  1>/home/jyz/app/logs/ruoyi-admin.log&"
#docker container prune -f
```

### 添加shell脚本（前端）

```shell
#!/bin/bash
cd /compliance/pages/compliance-pages/
git checkout master
git pull origin master
npm --unsafe-perm install
npm run build:prod --unsafe-perm
cp -r /compliance/pages/compliance-pages/dist /usr/local/nginx/html/compliance-dev/dist
chmod -R 777 /usr/local/nginx/html/compliance-dev/dist
/usr/local/nginx/sbin/nginx -s reload
#docker container prune -f
```

