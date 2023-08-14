# nacos适配国产信创达梦数据库及WEB中间件TongWEB
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
### maven本地仓库添加TongWEB依赖
略
TongWEB版本需为7.0.E.6_P4
### 添加TongWEB的license
使用自己的license替换`console/src/main/resources/license.dat`

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
1. maven无法获取达梦数据库连接驱动时，请尝试切换到阿里云maven镜像
2. 本项目仅测试过nacos单机部署，集群部署是否可用无法保证
