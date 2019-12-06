#### @ComponentScan 其实是跟 @Component 配套使用的

讲个例子,在仿(其实是抄)一个权限框架的时候,每个过滤器上只要标注@Component注解,就会将该过滤器加入到过滤规则中,但是我在仿的时候,上层应用自定义的过滤器老是不能自动加入到过滤规则
然后排查了很久发现在入口处,我的@ComponentScan是这样写的
```
@ComponentScan(basePackages = {"com.mengya.security"})
public class Application extends WebMvcConfigurerAdapter{
    ....
}
```

而我的demo包名是com.mengya.demo,自定义过滤器就在该包名下,正确的写法应该是这样的
```
```
@ComponentScan(basePackages = {"com.mengya.security","com.mengya.demo"})
public class Application extends WebMvcConfigurerAdapter{
    ....
}
```
难怪一直没办法自动加入过滤规则中