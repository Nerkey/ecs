# CentOS 6 EOL如何切换源

CentOS 6操作系统版本结束了生命周期（EOL），Linux社区已不再维护该操作系统版本。建议您升级操作系统至CentOS 7及以上，如果您的业务过渡期仍需要使用CentOS 6系统中的一些安装包，请根据下文切换CentOS 6的源。

2020年11月30日CentOS 6 EOL。按照社区规则，CentOS 6的源地址`http://mirror.centos.org/centos-6/`内容已移除，目前第三方的镜像站中均已移除CentOS 6的源。阿里云的源`http://mirrors.cloud.aliyuncs.com`和`http://mirrors.aliyun.com`也无法同步到CentOS 6的源。当您在阿里云上继续使用默认配置的CentOS 6的源会发生报错。报错示例如下图所示：

![centos 6 error](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3368796061/p187588.png)

您可以通过以下步骤，在CentOS 6操作系统中将源配置按照网络环境不同进行切换。

-   专有网络VPC类型实例需切换为`http://mirrors.cloud.aliyuncs.com/centos-vault/6.10/`源。
-   经典网络类型实例需切换为`http://mirrors.aliyuncs.com/centos-vault/6.10/`源。

1.  登录CentOS 6系统的ECS实例。

    具体操作，请参见[连接方式概述](/cn.zh-CN/实例/连接实例/连接方式概述.md)。

2.  运行以下命令编辑`CentOS-Base.repo`文件。

    ```
    vim /etc/yum.repos.d/CentOS-Base.repo 
    ```

3.  按i进入编辑模式，修改以下内容切换源。

    请根据实例不同的网络类型进行修改，具体内容如下：

    -   专有网络VPC类型实例

        ```
        [base]
        name=CentOS-6.10
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.cloud.aliyuncs.com/centos-vault/6.10/os/$basearch/
        gpgcheck=1
        gpgkey=http://mirrors.cloud.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6
        
        [updates]
        name=CentOS-6.10
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.cloud.aliyuncs.com/centos-vault/6.10/updates/$basearch/
        gpgcheck=1
        gpgkey=http://mirrors.cloud.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6
        
        [extras]
        name=CentOS-6.10
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.cloud.aliyuncs.com/centos-vault/6.10/extras/$basearch/
        gpgcheck=1
        gpgkey=http://mirrors.cloud.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6
        ```

    -   经典网络类型实例

        ```
        [base]
        name=CentOS-6.10
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.aliyuncs.com/centos-vault/6.10/os/$basearch/
        gpgcheck=1
        gpgkey=http://mirrors.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6
        
        [updates]
        name=CentOS-6.10
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.aliyuncs.com/centos-vault/6.10/updates/$basearch/
        gpgcheck=1
        gpgkey=http://mirrors.aliyuncs.comm/centos-vault/RPM-GPG-KEY-CentOS-6
        
        [extras]
        name=CentOS-6.10
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.aliyuncs.com/centos-vault/6.10/extras/$basearch/
        gpgcheck=1
        gpgkey=http://mirrors.aliyuncs.com/centos-vault/RPM-GPG-KEY-CentOS-6
        ```

    编辑完成后，按Esc键，并输入`:wq`保存退出文件。

4.  运行以下命令编辑`epel.repo`文件。

    ```
    vim /etc/yum.repos.d/epel.repo
    ```

5.  按i进入编辑模式，修改以下内容切换源。

    请根据实例不同的网络类型进行修改，具体内容如下：

    -   专有网络VPC类型实例

        ```
        [epel]
        name=Extra Packages for Enterprise Linux 6 - $basearch
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.cloud.aliyuncs.com/epel-archive/6/$basearch
        gpgcheck=0
        gpgkey=http://mirrors.cloud.aliyuncs.com/epel-archive/RPM-GPG-KEY-EPEL-6
        ```

    -   经典网络类型实例

        ```
        [epel]
        name=Extra Packages for Enterprise Linux 6 - $basearch
        enabled=1
        failovermethod=priority
        baseurl=http://mirrors.aliyuncs.com/epel-archive/6/$basearch
        gpgcheck=0
        gpgkey=http://mirrors.aliyuncs.com/epel-archive/RPM-GPG-KEY-EPEL-6
        ```

    编辑完成后，按Esc键，并输入`:wq`保存退出文件。

6.  切换完成后，您可以使用yum install命令安装需要的软件包。


**相关文档**  


[CentOS Product Specifications](https://wiki.centos.org/About/Product)

