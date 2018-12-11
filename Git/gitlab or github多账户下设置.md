>公司开发使用Gitlab,并且分配了新的账号.面临的问题就是Github的SSH KEY设置如何与GitLab的设置共存.
特别注意：以下命令均在 ~/.ssh 目录下执行
#### 生成SSH KEY
```
# Gitlab SSH KEY 生成命令
ssh-keygen -o -t rsa -C "your.email@example.com" -b 4096

# Github SSH KEY 生成命令
ssh-keygen -t rsa -C "your.email@example.com" 
```
在以下步骤时,如果直接enter键,默认生成的两个文件是(id_rsa和id_rsa.pub),因此要多账号共存,需要特别主要该步骤的设置,这里我们假设gitlab使用默认文件名，github使用(id_rsa_github)
```shell
>Enter file in which to save the key：id_rsa_github
```
#### 配置config
新建 config 文件
```shell
>touch config
```

#### 编辑config文件
>Host 可以随便填,HostName则是访问地址,不用携带端口(如果有域名直接使用域名)

```shell
# gitlab Host 可以随便填,HostName则是地址,不用携带端口(如果有域名直接使用域名)
Host gitlab.com 
    HostName xx.xx.xx.xx
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa
# github
Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_github
```

#### 测试是否成功

>如果以下命令返回Welcome或者successfully之类的消息则代表多账号配置成功
```
# 尝试访问github
ssh -T git@github.com

# 尝试访问gitlab
ssh -T git@xxxxxx.com
```