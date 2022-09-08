# mysql

## 安装

```
# 第一步 启动myl
docker run -p 3306:3306 --name mysql \
-v/mount/mysql/log:/var/log/mysql \
-v/mount/mysql/data:/var/lib/mysql \
-v/mount/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7

# 启动测试
docker run -p 3307:3306 --name cs1 \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7
# 将cs1 中/etc/mysql  文件复制到 /mount/mysql/conf路径中

# 删除 cs1
```



## 语法

### FIND_IN_SET

```sql
 #将cs 表中的ids 字符串作为检索条件 在sys_user 表中进行包含检索
select  * from  sys_user  where FIND_IN_SET(id,(select ids from cs where id =1))
```

