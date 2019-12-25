##### Springboot集成Mybatis

###### 一、配置相关
1. (Web)开启Spring Web
2. (SQL)开启MySQL Driver/开启MyBatis Framework

打开pom.xml文件,我们发现当前的Springboot的版本为：2.1.8.RELEASE,mybatis-spring-boot-starter模块的版本为:2.1.0,mybatis-spring-boot-starter版本与Springboot的版本存在一定的要求,你可以在[mybatis-spring-boot-autoconfigure
](http://mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/)查看版本对应关系.
```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.1.8.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>
...
<dependencies>
    ...
    <dependency>
        <groupId>org.mybatis.spring.boot</groupId>
        <artifactId>mybatis-spring-boot-starter</artifactId>
        <version>2.1.0</version>
    </dependency>
    ....
</dependencies>

```

##### 快速开始：
你可能已经知道,在Spring中使用Mybatis至少需要一个SqlSessionFactory和至少一个Mapper接口.
MyBatis-Spring-Boot-Starter插件会帮我们执行以下工作:
1. 自动检测现有的数据源
2. 使用该数据源作为输入传递(生成SqlSessionFactoryBean),通过以上数据创建并注册SqlSessionFactory.
3. 创建并注册从SqlSessionFactory获取到的SqlSessionTemplate.
4. 自动扫描你的Mapper接口,将其链接到SqlSessionTemplate，同时将Mappers注册到Spring Context（Spring 上下文），这样他们就可以注入到你的类中.

##### 进阶扫描
默认情况下,MyBatis-Spring-Boot-Starter插件将自动扫描带有@Mapper注解的Mapper接口.


##### 引入Druid数据源
Druid不仅提供了数据库连接池的功能,还提供了监控功能.
Druid在 0.1.18 之后版本都发布到maven中央仓库中,我们可以通过以下依赖来使用Druid的能力
```
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>${druid-version}</version>
</dependency>
```

