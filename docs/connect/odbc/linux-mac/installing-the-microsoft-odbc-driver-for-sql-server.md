---
title: 在 Linux 和 macOS 上安装 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 79c2276174f0e8f3474350c6c91fb4d3ede0401d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "76911218"
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>安装 Linux 和 macOS 上的 Microsoft ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文介绍如何在 Linux 和 macOS 上安装 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，以及适用于 SQL Server（`bcp` 和 `sqlcmd`）和 unixODBC 开发标头的可选命令行工具。

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 for SQL Server 

> [!IMPORTANT]
> 如果安装了暂时可用的 v17 `msodbcsql` 包，应先删除它，再安装 `msodbcsql17` 包。 这样可避免冲突。 `msodbcsql17` 包可以与 `msodbcsql` v13 包并行安装。

### <a name="alpine-linux"></a>Alpine Linux
```
#Download the desired package(s)
curl https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.1.1-1_amd64.apk
curl https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.1.1-1_amd64.apk


#(Optional) Verify signature, if 'gpg' is missing install it using 'apk add gnupg':
curl https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/msodbcsql17_17.5.1.1-1_amd64.sig
curl https://download.microsoft.com/download/e/4/e/e4e67866-dffd-428c-aac7-8d28ddafb39b/mssql-tools_17.5.1.1-1_amd64.sig

curl https://packages.microsoft.com/keys/microsoft.asc  | gpg --import -
gpg --verify msodbcsql_17.5.1.1-1_amd64.sig msodbcsql_17.5.1.1-1_amd64.apk


#Install the package(s)
sudo apk add --allow-untrusted msodbcsql_17.5.1.1-1_amd64.apk
sudo apk add --allow-untrusted mssql-tools_17.5.1.1-1_amd64.apk

```
> [!NOTE]
> - 必须有驱动程序版本 17.5 或更高版本，才能获得 Alpine 支持。

### <a name="debian"></a>Debian
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 10
curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
# optional: kerberos library for debian-slim distributions
sudo apt-get install libgssapi-krb5-2
```

> [!NOTE]
> - 可以将设置环境变量“ACCEPT_EULA”替换为设置 debconf 变量“msodbcsql/ACCEPT_EULA”：`echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`


### <a name="redhat-enterprise-server-and-oracle-linux"></a>RedHat Enterprise Server 和 Oracle Linux
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 8 and Oracle Linux 8
curl https://packages.microsoft.com/config/rhel/8/prod.repo > /etc/yum.repos.d/mssql-release.repo

exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server"></a>SUSE Linux Enterprise Server

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
#Ensure SUSE Linux Enterprise 11 Security Module has been installed 
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

#SUSE Linux Enterprise Server 15
zypper ar https://packages.microsoft.com/config/sles/15/prod.repo
#(Only for driver 17.3 and below)
SUSEConnect -p sle-module-legacy/15/x86_64

exit
sudo ACCEPT_EULA=Y zypper install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu"></a>Ubuntu
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 19.10
curl https://packages.microsoft.com/config/ubuntu/19.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql17
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```
> [!NOTE]
> - Ubuntu 18.04 支持需要 17.2 或更高版本的驱动程序。
> - Ubuntu 18.10 支持需要 17.3 或更高版本的驱动程序。

> [!NOTE]
> - 可以将设置环境变量“ACCEPT_EULA”替换为设置 debconf 变量“msodbcsql/ACCEPT_EULA”：`echo msodbcsql17 msodbcsql/ACCEPT_EULA boolean true | sudo debconf-set-selections`

### <a name="macos"></a>MacOS

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql17 mssql-tools
```

## <a name="microsoft-odbc-driver-131-for-sql-server"></a>Microsoft ODBC Driver 13.1 for SQL Server 

### <a name="debian-8"></a>Debian 8
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum remove unixODBC-utf16 unixODBC-utf16-devel #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y yum install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo yum install unixODBC-devel
```

### <a name="suse-linux-enterprise-server-11"></a>SUSE Linux Enterprise Server 11

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo
exit
sudo ACCEPT_EULA=Y zypper install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y zypper install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo zypper install unixODBC-devel
``` 

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="ubuntu-1610"></a>Ubuntu 16.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
# optional: for bcp and sqlcmd
sudo ACCEPT_EULA=Y apt-get install mssql-tools
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
# optional: for unixODBC development headers
sudo apt-get install unixodbc-dev
```

### <a name="os-x-1011-el-capitan-and-macos-1012-sierra"></a>OS X 10.11 (El Capitan) 和 macOS 10.12 (Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise Server 6
```
sudo su
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise Server 7
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC #to avoid conflicts
sudo ACCEPT_EULA=Y yum install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
sudo yum install unixODBC-utf16-devel #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1510"></a>Ubuntu 15.10
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="ubuntu-1604"></a>Ubuntu 16.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql=13.0.1.0-1 mssql-tools=14.0.2.0-1
sudo apt-get install unixodbc-dev-utf16 #this step is optional but recommended*
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12

```
sudo su 
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo 
zypper update 
sudo ACCEPT_EULA=Y zypper install msodbcsql-13.0.1.0-1 mssql-tools-14.0.2.0-1
zypper install unixODBC-utf16-devel
#Create symlinks for tools
ln -sfn /opt/mssql-tools/bin/sqlcmd-13.0.1.0 /usr/bin/sqlcmd 
ln -sfn /opt/mssql-tools/bin/bcp-13.0.1.0 /usr/bin/bcp
```

### <a name="offline-installation"></a>脱机安装
如果希望/需要在未连接 Internet 的计算机上安装 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13，则需要手动解析包依赖项。 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 具有以下直接依赖项：
- Ubuntu：libc6 (>= 2.21), libstdc++6 (>= 4.9), libkrb5-3, libcurl3, openssl, debconf (>= 0.5), unixodbc (>= 2.3.1-1)
- Red Hat：```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE：```glibc, libuuid1, krb5, openssl, unixODBC```

所有这些包都具有自己的依赖项，这些依赖性可能会显示在系统上，也可能不会显示。 有关此问题的常规解决方案，请参阅发行版对应的包管理器文档：[Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos)、[Ubuntu](https://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian) 和 [SUSE](https://en.opensuse.org/Portal:Zypper)

还有一种常见做法是，手动下载所有相关包并将其一起放置在安装计算机上，然后依次手动安装每个包，最后安装 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 包。

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - 从 https://packages.microsoft.com/rhel/7/prod/ 下载最新 `msodbcsql` `.rpm`
  - 安装依赖项和驱动程序
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- 从 https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 下载最新 `msodbcsql` `.deb` 
- 安装依赖项和驱动程序 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- 从 https://packages.microsoft.com/sles/12/prod/ 下载最新 `msodbcsql` `.rpm`
- 安装依赖项和驱动程序

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

完成包安装后，可以通过运行 ldd 并检查其输出是否缺少库来验证 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 是否可以找到其所有依赖项：
```
ldd /opt/microsoft/msodbcsql/lib64/libmsodbcsql-*
```
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-linux"></a>Linux 上的 Microsoft ODBC Driver 11 for SQL Server

安装 unixODBC 驱动程序管理器后才能开始使用该驱动程序。 有关详细信息，请参阅[安装驱动程序管理器](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)。

**安装步骤**  

> [!IMPORTANT]  
> 这些说明参考了 Red Hat Linux 的安装文件 `msodbcsql-11.0.2270.0.tar.gz`。 如果要安装适用于 SUSE Linux 的预览版，则文件名为 `msodbcsql-11.0.2260.0.tar.gz`。  
  
若要安装该驱动程序：

1.  请确保具有根权限。  

2.  转到下载放置文件 `msodbcsql-11.0.2270.0.tar.gz` 的目录。 确保所拥有的 \*.tar.gz 文件与你的 Linux 版本匹配。 若要提取文件，请执行以下命令：`tar xvzf msodbcsql-11.0.2270.0.tar.gz`。  
  
3.  转到 `msodbcsql-11.0.2270.0` 目录，你应在此处看到一个名为 install.sh 的文件  。  
  
4.  若要查看可用安装选项的列表，请执行以下命令： **./install.sh**。  
  
5.  创建 **odbcinst.ini**的备份。 驱动程序安装会更新 **odbcinst.ini**。 odbcinst.ini 包含在 unixODBC 驱动程序管理器中注册的驱动程序列表。 若要在计算机上发现 odbcinst.ini 的位置，请执行以下命令：```odbc_config --odbcinstini```。  
  
6.  安装该驱动程序之前，请执行以下命令：`./install.sh verify`。 `./install.sh verify` 告的输出会报计算机中是否具有在 Linux 上支持 ODBC 驱动程序所需的软件。  
  
7.  当你准备好在 Linux 上安装 ODBC 驱动程序时，请执行命令：`./install.sh install`。 如果需要指定安装命令（`bin-dir` 或 `lib-dir`），请在“安装”选项后指定该命令  。  
  
8.  查看许可协议之后，键入 **YES** 以继续安装。  
  
安装会将驱动程序放在 `/opt/microsoft/msodbcsql/11.0.2270.0` 中。 驱动程序及其支持文件必须位于 `/opt/microsoft/msodbcsql/11.0.2270.0` 中。  
  
若要验证 Linux 上的 Microsoft ODBC 驱动程序是否已成功注册，请执行以下命令：```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```。  
  
[对 Linux 上的 ODBC 驱动程序使用现有 MSDN C++ ODBC 示例](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 会使用 Linux 上的 ODBC 驱动程序显示一个连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的代码示例。  
  
**卸载**  
  
通过执行以下命令，可以卸载 Linux 上的 ODBC 驱动程序 11：  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>解决连接问题  
如果使用 ODBC 驱动程序无法连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请使用以下信息确定问题原因。  
  
最常见的连接问题是安装两个 UnixODBC 驱动程序管理器的副本。 搜索 /usr 以查找 libodbc\*.so\*。 如果看到多个版本的文件，则（可能）安装了多个驱动程序管理器。 你的应用程序可能会使用错误的版本。
  
通过编辑 `/etc/odbcinst.ini` 文件以包含具有这些条目的如下部分来启用连接日志：

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
如果连接再次失败并且未看到日志文件，则计算机上（可能）存在两个驱动程序管理器的副本。 否则，日志输出应该类似于以下内容：  
  
```  
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 13 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
如果 ASCII 字符编码不是 UTF-8，例如： 
  
```  
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
安装了多个驱动程序管理器并且应用程序使用的是错误的管理器，或者驱动程序管理器未正确构建。  
  
有关解决这种连接失败的详细信息，请参阅：  
  
-   [解决 SQL 连接问题的步骤](https://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [SQL Server 2005 连接问题疑难解答 - 第 I 部分](https://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [带有连接环形缓冲区的 SQL Server 2008 中的连接疑难解答](https://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [SQL Server 身份验证疑难解答](https://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [错误详细信息 (https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](https://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    应更改在 URL 中指定的错误号 (11001) 以与你看到的错误相匹配。  
  
## <a name="driver-files"></a>驱动程序文件
Linux 和 MacOS 上的 ODBC Driver 由以下组件构成：

### <a name="linux"></a>Linux

|组件|说明|  
|---------------|-----------------|  
|libmsodbcsql-17.X.so.X.X 或 libmsodbcsql-13.X.so.X.X|包含该驱动程序所有功能的共享对象 (`so`) 动态库文件。 此文件安装在 ODBC Driver 17 的 `/opt/microsoft/msodbcsql17/lib64/` 中和 ODBC Driver 13 的 `/opt/microsoft/msodbcsql/lib64/` 中。|  
|`msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`|驱动程序库的附带资源文件。 此文件安装在 `[driver .so directory]../share/resources/en_US/` 中| 
|msodbcsql.h|头文件，它包含使用驱动程序所需的所有新定义。<br /><br /> **注意：** 无法在同一个程序中引用 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 安装在 ODBC Driver 17 的 `/opt/microsoft/msodbcsql17/include/` 中和 ODBC Driver 13 的 `/opt/microsoft/msodbcsql/include/` 中。 |
|LICENSE.txt|包含最终用户许可协议条款的文本文件。 此文件位于 ODBC Driver 17 的 `/usr/share/doc/msodbcsql17/` 中和 ODBC Driver 13 的 `/usr/share/doc/msodbcsql/` 中。|
|RELEASE_NOTES|包含发行说明的文本文件。 此文件位于 ODBC Driver 17 的 `/usr/share/doc/msodbcsql17/` 中和 ODBC Driver 13 的 `/usr/share/doc/msodbcsql/` 中。|


### <a name="macos"></a>MacOS

|组件|说明|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib 或 libmsodbcsql.13.dylib|包含该驱动程序所有功能的动态库 (`dylib`) 文件。 此文件安装在 `/usr/local/lib/` 中。|  
|`msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`|驱动程序库的附带资源文件。 此文件安装在 ODBC Driver 17 的 `[driver .dylib directory]../share/msodbcsql17/resources/en_US/` 中和 ODBC Driver 13 的 `[driver .dylib directory]../share/msodbcsql/resources/en_US/` 中。 | 
|msodbcsql.h|头文件，它包含使用驱动程序所需的所有新定义。<br /><br /> **注意：** 无法在同一个程序中引用 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 安装在 ODBC Driver 17 的 `/usr/local/include/msodbcsql17/` 中和 ODBC Driver 13 的 `/usr/local/include/msodbcsql/` 中。 |
|LICENSE.txt|包含最终用户许可协议条款的文本文件。 此文件位于 ODBC Driver 17 的 `/usr/local/share/doc/msodbcsql17/` 中和 ODBC Driver 13 的 `/usr/local/share/doc/msodbcsql/` 中。 |
|RELEASE_NOTES|包含发行说明的文本文件。 此文件位于 ODBC Driver 17 的 `/usr/local/share/doc/msodbcsql17/` 中和 ODBC Driver 13 的 `/usr/local/share/doc/msodbcsql/` 中。 |

## <a name="resource-file-loading"></a>资源文件加载

驱动程序需要加载资源文件才能正常运行。 此文件称为 `msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`，具体取决于驱动程序版本。 `.rll` 文件的位置与驱动程序本身的位置（`so` 或 `dylib`）相对，如上表中所述。 自版本 17.1 开始，如果从相对路径加载失败，驱动程序还将尝试从默认目录加载 `.rll`。 默认资源文件路径为：

Linux：`/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS：`/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>另请参阅

[安装驱动程序管理器](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)

[系统要求](../../../connect/odbc/linux-mac/system-requirements.md)
