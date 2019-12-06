#### /bin/bash^m bad interpreter no such file or directory

这是通常是由于window迁移到unix系统时shell脚本编码导致的shell脚本运行错误
以下是快速解决办法

```
sed -i -e 's/\r$//' problem.sh
```

