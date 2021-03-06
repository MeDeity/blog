#### DockerFile文件制作基础指令

##### 一、FROM 指令
```
# 基础镜像
FROM centos
```
构建这个自定义镜像的基础镜像是什么,基础镜像所拥有的功能在自定义镜像中也是存在的.一般作为采用最干净的无修改的系统镜像为基础镜像,例如CentOS.

##### 二、MAINTAINER 维护者信息
```
MAINTAINER MeDeity
```
维护者信息展示

##### 三、ENV 设置环境变量
```
#ENV 设置环境变量
ENV PATH /usr/local/nginx/sbin:$PATH
```
常用WIN系统的同学可能经常遇到运行CMD命令时,经常提示找不到命令,ENV跟WIN系统的配置环境变量的PATH一样,当我们尝试运行未指定路径的命令时,系统会尝试在设置的PATH下查找需要运行的指令.


##### 四、ADD 添加文件功能
```
#ADD  文件放在当前目录下，拷过去会自动解压
ADD nginx-1.13.7.tar.gz /tmp/
```
添加文件功能,目标文件可以是一个文件、可以是一个URL地址.如果目标文件是一个压缩包,构建镜像时会自动解压
>需要特别注意的是，目标文件如果是文件,则必须在dockerfile文件目录内,不在文件目录内的,会提示找不到文件.

#### 五、RUN 执行命令
RUN 就是执行命令的意思.RUN可以使用&&隔开来执行多条命令,如果命令太长可以在尾部加上'\'来换行命令。
>dockerfile 构建镜像时每执行一个关键指令都会去创建一个镜像版本，这有点像 git 的版本管理，比如执行完第一个 RUN 命令后在执行第二个 RUN 命令时是会在一个新的镜像版本中执行,这里有个原则就是把所有相关的操作都放在同一个 RUN 里面

#### 六、WORKDIR 切换工作目录
这个命令有点像cd指令.
```
RUN cd /tmp/nginx-1.13.7
RUN ./configure
```
>需要说明的是以上是不行的。会报找不到configure的错误.因为这个两个命令都不是在同一个**镜像版本**中执行的,第一个镜像 cd 进入的目录并不代表后面的镜像也进入了


扩展链接
1. [如果编写DockerFile文件](https://juejin.im/post/5a1bd8a36fb9a0450f21a966)
2. [使用 Dockerfile 定制镜像](https://yeasy.gitbooks.io/docker_practice/image/build.html)