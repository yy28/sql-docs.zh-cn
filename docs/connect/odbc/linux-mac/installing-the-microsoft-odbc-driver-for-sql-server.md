---
title: 在 Linux 和 macOS 上安装 Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- driver, installing
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: ab32d1ac12bbe6f81241590a1e61b9579772cb7d
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784165"
---
# <a name="installing-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>安装 Linux 和 macOS 上的 Microsoft ODBC Driver for SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

本文介绍如何安装[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC 驱动程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]有关 Linux 和 macOS，以及适用于 SQL Server 的可选命令行工具 (`bcp`和`sqlcmd`) 和 unixODBC 开发标头。

## <a name="microsoft-odbc-driver-17-for-sql-server"></a>Microsoft ODBC Driver 17 for SQL Server 

> [!IMPORTANT]
> 如果您安装了 v17`msodbcsql`简要可用的包，您应将其删除然后再安装`msodbcsql17`包。 这可以避免冲突。 `msodbcsql17`可以并行安装包`msodbcsql`v13 包。

### <a name="debian-8-and-9"></a>Debian 8 和 9
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Debian 8
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Debian 9
curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list

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

### <a name="redhat-enterprise-server-6-and-7"></a>RedHat Enterprise Server 6 和 7
```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#RedHat Enterprise Server 6
curl https://packages.microsoft.com/config/rhel/6/prod.repo > /etc/yum.repos.d/mssql-release.repo

#RedHat Enterprise Server 7
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo

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

### <a name="suse-linux-enterprise-server-11sp4-and-12"></a>SUSE Linux Enterprise Server 11SP4 和 12

```
sudo su

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#SUSE Linux Enterprise Server 11 SP4
zypper ar https://packages.microsoft.com/config/sles/11/prod.repo

#SUSE Linux Enterprise Server 12
zypper ar https://packages.microsoft.com/config/sles/12/prod.repo

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

### <a name="ubuntu-1404-1604-1710-and-1804"></a>Ubuntu 14.04、 16.04、 17.10 和 18.04
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

#Download appropriate package for the OS version
#Choose only ONE of the following, corresponding to your OS version

#Ubuntu 14.04
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 16.04
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 17.10
curl https://packages.microsoft.com/config/ubuntu/17.10/prod.list > /etc/apt/sources.list.d/mssql-release.list

#Ubuntu 18.04
curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list

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
> Ubuntu 18.04 支持需要驱动程序版本 17.2 或更高版本。

### <a name="os-x-1011-el-capitan-macos-1012-sierra-and-macos-1013-high-sierra"></a>OS X 10.11 (El Capitan)、 macOS 10.12 (Sierra) 和 macOS 10.13 (High Sierra)

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox msodbcsql17 mssql-tools
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

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise 服务器 6
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

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise 服务器 7
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
brew install --no-sandbox msodbcsql@13.1.9.2 mssql-tools@14.0.6.0
```

## <a name="microsoft-odbc-driver-13-for-sql-server"></a>Microsoft ODBC Driver 13 for SQL Server

### <a name="redhat-enterprise-server-6"></a>RedHat Enterprise 服务器 6
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

### <a name="redhat-enterprise-server-7"></a>RedHat Enterprise 服务器 7
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
如果更喜欢/需要[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 若要在无 internet 连接的计算机上安装，你将需要手动解决包依赖项。 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 具有以下直接依赖项：
- Ubuntu: libc6 (> = 2.21)，libstdc + + 6 (> = 4.9)，libkrb5-3、 libcurl3、 openssl、 debconf (> = 0.5)，unixodbc (> = 2.3.1-1)
- Red Hat：```glibc, e2fsprogs, krb5-libs, openssl, unixODBC```
- SuSE：```glibc, libuuid1, krb5, openssl, unixODBC```

每个这些包反过来有其自己的依赖项，可能会或可能不会显示在系统上。 有关此问题的常规解决方案，请参阅分发的包管理器文档： [Redhat](https://wiki.centos.org/HowTos/CreateLocalRepos)， [Ubuntu](http://unix.stackexchange.com/questions/87130/how-to-quickly-create-a-local-apt-repository-for-random-packages-using-a-debian)，和[SUSE](https://en.opensuse.org/Portal:Zypper)

它也是很常见手动下载所有依赖包并将它们一起放安装在计算机上，然后手动安装反过来，每个包使用[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 包。

#### <a name="redhat-linux-enterprise-server-7"></a>Redhat Linux Enterprise Server 7
  - 下载最新`msodbcsql``.rpm`从此处： http://packages.microsoft.com/rhel/7/prod/
  - 安装依赖项和驱动程序
  
```
yum install glibc e2fsprogs krb5-libs openssl unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

#### <a name="ubuntu-1604"></a>Ubuntu 16.04
- 下载最新`msodbcsql``.deb`从此处： http://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/ 
- 安装依赖项和驱动程序 

```
sudo apt-get install libc6 libstdc++6 libkrb5-3 libcurl3 openssl debconf unixodbc unixodbc-dev #install dependencies
sudo dpkg -i msodbcsql_13.1.X.X-X_amd64.deb #install the Driver
```

#### <a name="suse-linux-enterprise-server-12"></a>SUSE Linux Enterprise Server 12
- 下载最新`msodbcsql``.rpm`从此处： http://packages.microsoft.com/sles/12/prod/
- 安装依赖项和驱动程序

```
zypper install glibc, libuuid1, krb5, openssl, unixODBC unixODBC-devel #install dependencies
sudo rpm -i  msodbcsql-13.1.X.X-X.x86_64.rpm #install the Driver
```

完成包安装后，你可以验证[!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver 13 可以通过运行 ldd 并检查其输出的缺少库来查找其所有依赖项：
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

2.  将更改为下载放置文件的目录`msodbcsql-11.0.2270.0.tar.gz`。 确保所拥有的 \*.tar.gz 文件与你的 Linux 版本匹配。 若要提取文件，请执行以下命令：`tar xvzf msodbcsql-11.0.2270.0.tar.gz`。  
  
3.  转到 `msodbcsql-11.0.2270.0` 目录，你应在此处看到一个名为 install.sh 的文件。  
  
4.  若要查看可用安装选项的列表，请执行以下命令： **./install.sh**。  
  
5.  创建 **odbcinst.ini**的备份。 驱动程序安装会更新 **odbcinst.ini**。 odbcinst.ini 包含在 unixODBC 驱动程序管理器中注册的驱动程序列表。 若要在计算机上发现 odbcinst.ini 的位置，请执行以下命令：```odbc_config --odbcinstini```。  
  
6.  安装该驱动程序之前，请执行以下命令：`./install.sh verify`。 `./install.sh verify` 告的输出会报计算机中是否具有在 Linux 上支持 ODBC 驱动程序所需的软件。  
  
7.  当你准备好在 Linux 上安装 ODBC 驱动程序时，请执行命令：`./install.sh install`。 如果需要指定安装命令（`bin-dir` 或 `lib-dir`），请在“安装”选项后指定该命令。  
  
8.  查看许可协议之后，键入 **YES** 以继续安装。  
  
安装将驱动程序放置`/opt/microsoft/msodbcsql/11.0.2270.0`。 该驱动程序和及其支持文件必须位于`/opt/microsoft/msodbcsql/11.0.2270.0`。  
  
若要验证 Linux 上的 Microsoft ODBC 驱动程序是否已成功注册，请执行以下命令：```odbcinst -q -d -n "ODBC Driver 11 for SQL Server"```。  
  
[对 Linux 上的 ODBC 驱动程序使用现有 MSDN C++ ODBC 示例](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) 会使用 Linux 上的 ODBC 驱动程序显示一个连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的代码示例。  
  
**卸载**  
  
通过执行以下命令，可以卸载 Linux 上的 ODBC 驱动程序 11：  
  
1.  `rm -f /usr/bin/sqlcmd`
  
2.  `rm -f /usr/bin/bcp`  
  
3.  `rm -rf /opt/microsoft/msodbcsql`  
  
4.  `odbcinst -u -d -n "ODBC Driver 11 for SQL Server"`
  
## <a name="troubleshooting-connection-problems"></a>解决连接问题  
如果使用 ODBC 驱动程序无法连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，请使用以下信息确定问题原因。  
  
最常见的连接问题是安装两个 UnixODBC 驱动程序管理器的副本。 搜索 /usr 以查找 libodbc\*.so\*。 如果看到多个版本的文件，则（可能）安装了多个驱动程序管理器。 你的应用程序可能会使用错误的版本。
  
通过编辑来启用连接日志在`/etc/odbcinst.ini`文件应包含具有以下这些项目的以下部分：

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
  
没有多个安装的驱动程序管理器和你的应用程序使用了一个，或驱动程序管理器没有正确生成的错误。  
  
有关解决这种连接失败的详细信息，请参阅：  
  
-   [解决 SQL 连接问题的步骤](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
-   [SQL Server 2005 连接问题疑难解答 - 第 I 部分](http://blogs.msdn.com/b/sql_protocols/archive/2005/10/22/sql-server-2005-connectivity-issue-troubleshoot-part-i.aspx)  
  
-   [带有连接环形缓冲区的 SQL Server 2008 中的连接疑难解答](http://blogs.msdn.com/b/sql_protocols/archive/2008/05/20/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer.aspx)  
  
-   [SQL Server 身份验证疑难解答](http://blogs.msdn.com/b/sqlsecurity/archive/2010/03/29/sql-server-authentication-troubleshooter.aspx)  
  
-   [错误详细信息 (http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=11001)](http://www.microsoft.com/products/ee/transform.aspx?ProdName=Microsoft+SQL+Server&EvtSrc=MSSQLServer&EvtID=001)  
  
    应更改在 URL 中指定的错误号 (11001) 以与你看到的错误相匹配。  
  
## <a name="driver-files"></a>驱动程序文件
在 Linux 和 MacOS 上 ODBC 驱动程序由以下组件构成：

### <a name="linux"></a>Linux

|组件|描述|  
|---------------|-----------------|  
|libmsodbcsql 17。X.so.X.X 或 libmsodbcsql 13。X.so.X.X|包含该驱动程序所有功能的动态库 (`so`) 文件。 此文件安装在`/opt/microsoft/msodbcsql17/lib64/`Driver 17 并在`/opt/microsoft/msodbcsql/lib64/`为 Driver 13。|  
|`msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`|驱动程序库的附带资源文件。 此文件安装在 `[driver .so directory]../share/resources/en_US/`| 
|msodbcsql.h|头文件，它包含使用驱动程序所需的所有新定义。<br /><br /> **注意：**  你无法在同一个程序中引用 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 安装在`/opt/microsoft/msodbcsql17/include/`Driver 17 并在`/opt/microsoft/msodbcsql/include/`为 Driver 13。 |
|LICENSE.txt|包含最终用户许可协议的条款的文本文件。 此文件放在`/usr/share/doc/msodbcsql17/`Driver 17 并在`/usr/share/doc/msodbcsql/`为 Driver 13。|
|RELEASE_NOTES|包含发行说明的文本文件。 此文件放在`/usr/share/doc/msodbcsql17/`Driver 17 并在`/usr/share/doc/msodbcsql/`为 Driver 13。|


### <a name="macos"></a>MacOS

|组件|描述|  
|---------------|-----------------|  
|libmsodbcsql.17.dylib 或 libmsodbcsql.13.dylib|包含该驱动程序所有功能的动态库 (`dylib`) 文件。 此文件安装在`/usr/local/lib/`。|  
|`msodbcsqlr17.rll` 或 `msodbcsqlr13.rll`|驱动程序库的附带资源文件。 此文件安装在`[driver .dylib directory]../share/msodbcsql17/resources/en_US/`Driver 17 并在`[driver .dylib directory]../share/msodbcsql/resources/en_US/`为 Driver 13。 | 
|msodbcsql.h|头文件，它包含使用驱动程序所需的所有新定义。<br /><br /> **注意：**  你无法在同一个程序中引用 msodbcsql.h 和 odbcss.h。<br /><br /> msodbcsql.h 安装在`/usr/local/include/msodbcsql17/`Driver 17 并在`/usr/local/include/msodbcsql/`为 Driver 13。 |
|LICENSE.txt|包含最终用户许可协议的条款的文本文件。 此文件放在`/usr/local/share/doc/msodbcsql17/`Driver 17 并在`/usr/local/share/doc/msodbcsql/`为 Driver 13。 |
|RELEASE_NOTES|包含发行说明的文本文件。 此文件放在`/usr/local/share/doc/msodbcsql17/`Driver 17 并在`/usr/local/share/doc/msodbcsql/`为 Driver 13。 |

## <a name="resource-file-loading"></a>资源文件加载

该驱动程序需要才能正常加载资源文件。 此文件称为`msodbcsqlr17.rll`或`msodbcsqlr13.rll`具体取决于驱动程序版本。 位置`.rll`文件是相对于驱动程序本身的位置 (`so`或`dylib`)，如上述表中所述。 自版本 17.1 驱动程序也会尝试加载`.rll`从默认目录，如果从相对路径加载失败。 默认资源文件路径是：

Linux：`/opt/microsoft/msodbcsql17/share/resources/en_US/`

MacOS：`/usr/local/share/msodbcsql17/resources/en_US/`


  
## <a name="see-also"></a>另请参阅

[安装驱动程序管理器](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)

[系统要求](../../../connect/odbc/linux-mac/system-requirements.md)
