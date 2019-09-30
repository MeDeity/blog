Mybatis-PageHelper是由abel533编写的一个Mybatis分页插件.

使用Mave方式引入分页插件
```
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper</artifactId>
    <version>最新版本</version>
</dependency>
```
> 你可以在这里查询最新版本的版本号

#### 配置拦截器
拦截器的配置目前提供以下两种方式
##### 一、[在MyBatis配置 xml] 中配置拦截器插件
```
<!-- 
    plugins在配置文件中的位置必须符合要求，否则会报错，顺序如下:
    properties?, settings?, 
    typeAliases?, typeHandlers?, 
    objectFactory?,objectWrapperFactory?, 
    plugins?, 
    environments?, databaseIdProvider?, mappers?
-->
<plugins>
    <!-- com.github.pagehelper为PageHelper类所在包名 -->
    <plugin interceptor="com.github.pagehelper.PageInterceptor">
        <!-- 使用下面的方式配置参数，后面会有所有的参数介绍 -->
        <property name="param1" value="value1"/>
	</plugin>
</plugins>
```
##### 二、在 Spring 配置文件中配置拦截器插件
使用 spring 的属性配置方式，可以使用 plugins 属性像下面这样配置：
```
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
  <!-- 注意其他配置 -->
  <property name="plugins">
    <array>
      <bean class="com.github.pagehelper.PageInterceptor">
        <property name="properties">
          <!--使用下面的方式配置参数，一行配置一个 -->
          <value>
            params=value1
          </value>
        </property>
      </bean>
    </array>
  </property>
</bean>
```
#### 三、常用参数介绍
大部分的参数介绍都可以在官网上[Mybatis-PageHelper](https://github.com/pagehelper/Mybatis-PageHelper/blob/master/wikis/zh/HowToUse.md)得到解答.


#### 扩展阅读:
[MyBatis中文文档](https://mybatis.org/mybatis-3/zh/)