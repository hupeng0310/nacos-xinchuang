# nacos适配国产信创达梦数据库及WEB中间件TongWEB
## nacos二进制包下载
[Nacos-1.4.1-DM RELEASE](https://github.com/hupeng0310/nacos-xinchuang/releases)

## nacos源码构建
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
### maven本地仓库添加TongWEB依赖
略
TongWEB版本需为7.0.E.6_P4
### 添加TongWEB的license
使用自己的license替换`console/src/main/resources/license.dat`

### nacos本地仓库添加达梦数据库驱动依赖
```shell
mvn install:install-file -Dfile=.\DmJdbcDriver18.jar -DgroupId=com.dameng -DartifactId=Dm8JdbcDriver18 -Dversion=8.1.1.193 -Dpackaging=jar
```

### nacos构建
```shell
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
1. startup.sh及shutdown.sh在windows环境下构建可能存在换行符问题无法在linux机器执行，需修改脚本换行符
2. 本项目仅测试过nacos单机部署，集群部署是否可用无法保证
