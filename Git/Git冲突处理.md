#### 保留本地更改,同步服务器新增内容(以本地为准),冲突手动处理
在较为开发过程中,碰到配置文件发生变更,又需要同步服务器代码,尝试git pull命名后,出现以下错误：
```
error: Your local changes to the following files would be overwritten by merge:
        ************
Please commit your changes or stash them before you merge.
Aborting
```
如果希望保留本地的改动,仅并入服务器新修改的配置项,可以尝试使用以下命令
```
git stash
git pull ****
git stash pop
```
#### 使用服务器覆盖本地更改
同时存在本地修改和服务器修改,如果想用服务上的变更覆盖本地修改,可使用以下命令:
```
git reset --hard
git pull ****
```
