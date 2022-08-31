# nginx

## liunx 安装

```sell
#下载
 wget -c https://nginx.org/download/nginx-1.12.0.tar.gz
#解压
tar -zxvf nginx-1.12.0.tar.gz
# 进入目录
cd nginx-1.12.0

#安装其他依赖
yum install pcre-devel zlib zlib-devel openssl openssl-devel
#安装编译器
yum install gcc -y

指定编译
CC=gcc
export CC
#配置
./configure
安装
make && make install
#查找安装目录
whereis nginx
# 进入安装目录
cd /usr/local/nginx/sbin/

# 启动命令 在/usr/local/nginx/sbin目录下执行
./nginx

# 关闭命令 在/usr/local/nginx/sbin目录下执行
./nginx -s stop

# 重新加载命令 在/usr/local/nginx/sbin目录下执行
./nginx -s reload
```





## nginx配置https

```

user  nginx;
worker_processes  2;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
    
	server {
	    listen 443 ssl;
	    listen 80;
		#填写绑定证书的域名
		server_name zbobo.xyz; 
		#证书文件名称
		ssl_certificate  /etc/nginx/ssl/zbobo.xyz_bundle.crt; 
		#私钥文件名称
		ssl_certificate_key /etc/nginx/ssl/zbobo.xyz.key; 
		ssl_session_timeout 5m;
		ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
		ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
		ssl_prefer_server_ciphers on;
		location / {

			proxy_pass http://1.116.22.15:8000;
			proxy_set_header Host $host;
			proxy_set_header X-Real-IP $remote_addr;
			proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
			proxy_set_header X-Forwarded-Proto $scheme;
	  	}
	  		# 加入robots.txt 防止搜索引擎爬虫抓取
	        location = /robots.txt {
	            root /home/wwwroot/Bitwarden;
	        }
	  
#		  location /notifications/hub {
#			proxy_pass http://1.116.22.15:3012;
#			proxy_set_header Upgrade $http_upgrade;
#			proxy_set_header Connection "upgrade";
#		  }
		  
#		  location /notifications/hub/negotiate {
#			proxy_pass http://1.116.22.15:8000;
#		  }
	}
#	server {
#		listen 80;
#		#填写绑定证书的域名
#		server_name zbobo.xyz; 
#		#把http的域名请求转成https
#		return 301 https://$host$request_uri; 
#	}
	
}

```

