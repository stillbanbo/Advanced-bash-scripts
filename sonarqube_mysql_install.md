## mysql install
### ubuntu20.04安装mysql 5.7.x
参考网站：https://zhuanlan.zhihu.com/p/348317883
关键点在于一个一个安装，会提示有啥依赖，就先装需要依赖的。
装好后：
```
mysql> create database sonar;
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sonar              |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
mysql> drop user 'sonar'@'localhost';
Query OK, 0 rows affected (0.01 sec)

mysql> CREATE USER 'sonar'@'localhost' IDENTIFIED BY '123456' PASSWORD EXPIRE NEVER;
Query OK, 0 rows affected (0.01 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.01 sec)
mysql> GRANT ALL PRIVILEGES ON sonar.* TO 'sonar'@'localhost';
```
## sonarqube install
```
# 需要修改的地方，要和mysql用户密码对应。
/opt/sonarqube-6.7.4$ sudo vi conf/sonar.properties
sonar.jdbc.username=root
sonar.jdbc.password=123456
sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance&useSSL=false
sonar.web.port=9055

```
