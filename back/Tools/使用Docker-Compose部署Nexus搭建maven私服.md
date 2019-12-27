#### 一、Nexus安装
目前测试使用的搭建环境为CentOS7,请确保环境安装了docker-compose,使用的docker-compose脚本如下:
```
version: '3'
services:
  nexus3:
    image: sonatype/nexus3
    container_name: nexus3
    volumes:
      - './nexus-data:/nexus-data:rw'
    ports:
      - '8081:8081'
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "10"
    restart: always  
```
部署成功后，使用http://ip:8081进行访问,初始密码为 admin/admin123


#### 二、maven项目如何指定使用私有仓库进行下载依赖库
以下方式可以二选一:
1. 在项目的pom.xml文件中添加repository配置
```
<!--在项目中指定使用私有仓库-->
<repositories>
    <repository>
        <id>nexus-private</id>
        <name>nexus-private</name>
        <url>http://IP:8081/repository/maven-public/</url>
    </repository>
</repositories>
```
2. 在~/.m2/settings中指定mirror
```
<mirrors>
    <!--其他镜像配置-->
    .....
    
    <!--使用自己的私有镜像-->
    <mirror>
        <id>nexus-private</id>
        <name>nexus-private</name>
        <url>http://IP:8081/repository/maven-public/</url>
        <mirrorOf>*</mirrorOf>
    </mirror>

</mirrors>
```

#### 三、发布自己的依赖库到私有仓库
在~/.m2/settings中增加server节点,根据需要可以添加多个server
```
<servers>
    <server>
      <id>nexus-private</id>
      <username>admin</username>
      <password>admin123</password>
    </server>
  </servers>
```
在项目的pom.xml 的build节点中配置maven-deploy-plugin插件
```
<!--发布到私有仓库依赖的插件-->
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-deploy-plugin</artifactId>
    <version>2.8.1</version>
    <configuration>
        <!--如果在多模块项目中，可以将不需要发布的项目配置为skip=true-->
        <skip>false</skip>
    </configuration>
</plugin>
```
在项目的pom.xml中配置distributionManagement
```
<!--发布到私有仓库的配置-->
<distributionManagement>
    <repository>
        <id>nexus-private</id>
        <name>nexus-private-releases</name>
        <url>http://IP:8081/repository/maven-releases/</url>
    </repository>
    <snapshotRepository>
        <id>nexus-private</id>
        <name>nexus-private-snapshots</name>
        <url>http://IP:8081/repository/maven-snapshots/</url>
        <uniqueVersion>false</uniqueVersion>
        <layout>legacy</layout>
    </snapshotRepository>
</distributionManagement>
```
>其中repository.id指~/.m2/settings.xml中配置的server.id, 这两个是同一个概念，值要一致

运行pom.xml所在目录 运行发布命令

 ~~mvn clean deploy -Dmaven.test.skip=true~~
```
mvn jar:jar deploy:deploy
```
>经试验使用`mvn jar:jar deploy:deploy`上传jar包成功, ~~mvn clean deploy -Dmaven.test.skip=true~~上传失败了,**目前尚不知道原因所在**

参考链接:
[Maven私有仓库-使用docker部署Nexus](https://www.cnblogs.com/fuhongwei041/p/7419450.html)


关于swap交换区的配置
```
#进入一个文件夹
cd /var
#（创建4GB的swap ,一般是内存的两倍）
dd if=/dev/zero of=swapfile bs=1024 count=4096000
# 创建swap文件
/sbin/mkswap swapfile
# 激活swap文件
/sbin/swapon swapfile
# 检查swap是否正确
/sbin/swapon -s 
# 加到fstab文件中让系统引导时自动启动
vim  /etc/fstab
```
在末尾增加以下内容：
>/var/swapfile swap swap defaults 0 0
```
reboot
free -m
```

[上传到私有仓库](https://stackoverflow.com/questions/6308162/maven-the-packaging-for-this-project-did-not-assign-a-file-to-the-build-artifac)