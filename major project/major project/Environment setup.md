## 环境搭建

#### MySQL安装

* 卸载内置环境

    ```bash
    ps axj | grep mariadb #检查是否有mariadb
    systemctl stop mariadb.service #停止mariadb服务如果有的话
    rpm -qa | grep mariadb
    rpm -qa | grep mysql #检查系统的安装包
    yum remove +安装包名 #卸载搜索出来的对应的安装包
    wget http://repo.mysql.com/mysql57-community-release-el7-10.noarch.rpm #获取mysql官方yum源
    ```

* 安装MySQL yum源

    ```bash
    rpm -Uvh mysql57-community-release-el7-10.noarch.rpm
    ```

* 安装

    ```bash
    yum install -y mysql-community-server
    ```

* 检查安装

    ```bash
    mysql --version
    ```

    

#### ipvsadm工具安装

* ```bash
    yum install ipvsadm
    ```

    

#### nginx服务器安装：

* ```bash
    yum install yum-utils
    vim /etc/yum.repos.d/nginx.repo
    yum install nginx
    ```

在编辑文件时，将以下内容放入文件中

[nginx-stable]

name=nginx stable repo

baseurl=http://nginx.org/packages/centos/$releasever/$basearch/

gpgcheck=1

enabled=1

gpgkey=https://nginx.org/keys/nginx_signing.key

module_hotfixes=true

[nginx-mainline]

name=nginx mainline repo

baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/

gpgcheck=1

enabled=0

gpgkey=https://nginx.org/keys/nginx_signing.key

module_hotfixes=true



#### 网卡配置

###### LVS服务器主机网卡配置

```bash
vim /etc/sysconfig/network-scripts/ifcfg-ens36
```

![{A5167DE5-BFF0-43cc-A8E1-3A2B4A51AE4F}](photo.assets/{A5167DE5-BFF0-43cc-A8E1-3A2B4A51AE4F}-17187816461824.png)

```bash
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```

![{185796F3-3A2A-4aba-839C-48DFA20CF445}-17187699127562](photo.assets/{185796F3-3A2A-4aba-839C-48DFA20CF445}-17187699127562-17187816658477.png)



###### nginx服务器主机网卡配置

```bash
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```

![{BFA06218-2247-480e-B65E-3CDC1ED33667}](photo.assets/{BFA06218-2247-480e-B65E-3CDC1ED33667}-171878169678210.png)

* 另一台nginx只需将IP改为192.168.222.136即可

###### 客户端网卡配置

```bash
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```

![{E4AD8F57-BCAD-4f9f-ACEE-83453132E554}](photo.assets/{E4AD8F57-BCAD-4f9f-ACEE-83453132E554}-171878171146013.png)


