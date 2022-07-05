# mysql

## 安装

## 语法

### FIND_IN_SET

```sql
 #将cs 表中的ids 字符串作为检索条件 在sys_user 表中进行包含检索
select  * from  sys_user  where FIND_IN_SET(id,(select ids from cs where id =1))
```

