# nacos适配国产信创达梦数据库
## nacos单机部署
### 执行nacos初始化sql
`conf/nacos-dm.sql`
### 配置文件修改
`conf/application.properties`
```properties
spring.datasource.platform=dm
db.num=1
db.driver=dm.jdbc.driver.DmDriver
db.url.0=jdbc:dm://xxxx:5236/
db.user.0=nacos
db.password.0=nacos
```
### nacos构建
```shell
# 将达梦数据库jdbc驱动添加到本地maven仓库
mvn install:install-file -Dfile=.\DmJdbcDriver18.jar -DgroupId=com.dameng -DartifactId=Dm8JdbcDriver18 -Dversion=8.1.1.193 -Dpackaging=jar
# 打包nacos 打包后的文件在/distribution/target/目录下
mvn -Prelease-nacos -Dmaven.test.skip=true -Drat.skip=true clean install -U
```
--- 
windows环境下构建需使用cmd, powershell无法执行该命令
### 启动nacos
```shell
cd /nacos/bin
sh startup.sh -m standalone
```
---
***注***<br/>
本项目仅测试过nacos单机部署，集群部署是否可用无法保证
