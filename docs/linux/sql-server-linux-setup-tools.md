---
title: 在 Linux 上安装 SQL Server 命令行工具 |Microsoft Docs
description: 本文介绍如何在 Linux 上安装 SQL Server 工具。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 4dc9dd24bc3bdfa918ffdc7d02688303d8dcde5e
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394845"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>在 Linux 上安装 sqlcmd 和 bcp SQL Server 命令行工具

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

通过下列步骤安装命令行工具、Microsoft ODBC 驱动程序及其依赖项。 **Mssql 工具**包包含：

- **sqlcmd**： 命令行查询实用程序。
- **bcp**： 大容量导入导出实用程序。

为以下平台安装工具：

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)
- [macOS](#macos)
- [Docker](#docker)

本文介绍如何安装命令行工具。 如果您正在寻找有关如何使用的示例**sqlcmd**或**bcp**，请参阅[链接](#next-steps)本主题末尾处。

## <a name="a-idrhelainstall-tools-on-rhel-7"></a><a id="RHEL"><a/>在 RHEL 7 上安装工具

使用以下步骤来安装**mssql 工具**Red Hat Enterprise Linux 上。 

1. 进入超级用户模式。

   ```bash
   sudo su
   ```

1. 下载 Microsoft Red Hat 存储库配置文件。

   ```bash
   curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo
   ```

1. 退出超级用户模式。

   ```bash
   exit
   ```

1. 如果你有旧版**mssql 工具**安装，请删除任何较旧的 unixODBC 包。

   ```bash
   sudo yum remove mssql-tools unixODBC-utf16-devel
   ```

1. 运行以下命令以安装**mssql 工具**使用 unixODBC 开发人员包。

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 若要更新到最新版**mssql 工具**运行以下命令：
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **可选**： 添加`/opt/mssql-tools/bin/`到你**路径**bash shell 中的环境变量。

   若要使**sqlcmd/bcp**可从登录会话的 bash shell 访问修改你**路径**中 **~/.bash_profile**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要使**sqlcmd/bcp**能从交互式/非登录会话，bash shell 访问修改**路径**中 **~/.bashrc**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="ubuntu"></a>在 Ubuntu 16.04 上安装工具

使用以下步骤来安装**mssql 工具**Ubuntu 上。 

1. 导入公共存储库 GPG 密钥。

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 注册 Microsoft Ubuntu 存储库。

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
   ```

1. 更新源列表，并使用 unixODBC 开发人员包运行安装命令。

   ```bash
   sudo apt-get update 
   sudo apt-get install mssql-tools unixodbc-dev
   ```

   > [!Note] 
   > 若要更新到最新版**mssql 工具**运行以下命令：
   >    ```bash
   >   sudo apt-get update 
   >   sudo apt-get install mssql-tools 
   >   ```

1. **可选**： 添加`/opt/mssql-tools/bin/`到你**路径**bash shell 中的环境变量。

   若要使**sqlcmd/bcp**可从登录会话的 bash shell 访问修改你**路径**中 **~/.bash_profile**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要使**sqlcmd/bcp**能从交互式/非登录会话，bash shell 访问修改**路径**中 **~/.bashrc**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="SLES"></a>在 SLES 12 上安装工具

使用以下步骤来安装**mssql 工具**SUSE Linux Enterprise Server 上。 

1. 将 Microsoft SQL Server 存储库添加到 Zypper。

   ```bash
   sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo 
   sudo zypper --gpg-auto-import-keys refresh
   ```

1. 安装**mssql 工具**使用 unixODBC 开发人员包。

   ```bash
   sudo zypper install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 若要更新到最新版**mssql 工具**运行以下命令：
   >    ```bash
   >   sudo zypper refresh
   >   sudo zypper update mssql-tools
   >   ```

1. **可选**： 添加`/opt/mssql-tools/bin/`到你**路径**bash shell 中的环境变量。

   若要使**sqlcmd/bcp**可从登录会话的 bash shell 访问修改你**路径**中 **~/.bash_profile**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   ```

   若要使**sqlcmd/bcp**能从交互式/非登录会话，bash shell 访问修改**路径**中 **~/.bashrc**文件使用以下命令：

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

## <a id="macos"></a> 在 macOS 上安装工具

预览**sqlcmd**并**bcp**现可在 macOS 上。 有关详细信息，请参阅[公告](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/16/sql-server-command-line-tools-for-macos-released/)。

*安装[Homebrew](https://brew.sh)如果你还没有它：*

        /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

要为 Mac El Capitan 和 Sierra 安装工具，请执行下列命令：

```
# brew untap microsoft/mssql-preview if you installed the preview version 
brew tap microsoft/mssql-release https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install --no-sandbox mssql-tools
#for silent install: 
#ACCEPT_EULA=y brew install --no-sandbox mssql-tools
```

## <a id="docker"></a> Docker

从 SQL Server 2017 CTP 2.0 开始，Docker 映像中便加入了 SQL Server 命令行工具。 如果使用交互式命令提示符附加至此映像，则可在本地运行工具。

## <a name="offline-installation"></a>脱机安装

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

下表提供了最新工具包的位置：

| 工具包 | 版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 工具包 | 14.0.5.0-1 | [mssql-tools RPM 包](https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| SLES RPM 工具包 | 14.0.5.0-1 | [mssql-tools RPM 包](https://packages.microsoft.com/sles/12/prod/mssql-tools-14.0.5.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 工具包 | 14.0.5.0-1 | [mssql-tools Debian 包](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |
| Ubuntu 16.10 Debian 工具包 | 14.0.5.0-1 | [mssql-tools Debian 包](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/mssql-tools/mssql-tools_14.0.5.0-1_amd64.deb) |

这些包依赖于**msodbcsql**，且必须先安装。 **Msodbcsql**程序包还具有一个依赖项上**unixODBC 开发**(RPM) 或**unixodbc 开发人员**(Debian)。 位置**msodbcsql**下表中列出的包：

| msodbcsql 包 | 版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM msodbcsql 包 | 13.1.6.0-1 | [msodbcsql RPM 包](https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| SLES RPM msodbcsql 包 | 13.1.6.0-1 | [msodbcsql RPM 包](https://packages.microsoft.com/sles/12/prod/msodbcsql-13.1.6.0-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian msodbcsql 包 | 13.1.6.0-1 | [msodbcsql Debian 包](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |
| Ubuntu 16.10 Debian msodbcsql 包 | 13.1.6.0-1 | [msodbcsql Debian 包](https://packages.microsoft.com/ubuntu/16.10/prod/pool/main/m/msodbcsql/msodbcsql_13.1.6.0-1_amd64.deb) |

若要手动安装这些包，请按照下列步骤操作：

1. **将下载的包移到 Linux 计算机**。 如果使用另一台计算机下载包，将包移到 Linux 计算机的一种方法是使用**scp**命令。

1. **安装和包**： 安装**mssql 工具**并**msodbc**包。 如果遇到任何依赖关系错误，请忽略，直到出现下一步操作。

    | 平台 | 包安装命令 |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | SLES | `sudo zypper install msodbcsql-13.1.6.0-1.x86_64.rpm`<br/>`sudo zypper install mssql-tools-14.0.5.0-1.x86_64.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_13.1.6.0-1_amd64.deb`<br/>`sudo dpkg -i mssql-tools_14.0.5.0-1_amd64.deb` |

1. **解决缺少的依赖项**： 必须在此时缺少依赖项。 如果没有，可以跳过此步骤。 在某些情况下，必须手动查找并安装这些依赖项。

    对于 RPM 包，可通过下列命令检查必需的依赖项：

    ```bash
    rpm -qpR msodbcsql-13.1.6.0-1.x86_64.rpm
    rpm -qpR mssql-tools-14.0.5.0-1.x86_64.rpm
    ```

    对于 Debian 包，如果你有权访问已批准存储库包含这些依赖项，最简单的解决方案是使用**apt get**命令：

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > 使用命令还会完成 SQL Server 包的安装。

    如果此操作对 Debian 包不起作用，可通过下列命令检查必需的依赖项：

    ```bash
    dpkg -I msodbcsql_13.1.6.0-1_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_14.0.5.0-1_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>后续步骤

有关如何使用的示例**sqlcmd**若要连接到 SQL Server 并创建一个数据库，请参阅以下快速入门：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)

有关如何使用的示例**bcp**大容量导入和导出数据，请参阅[大容量数据复制到 Linux 上的 SQL Server](sql-server-linux-migrate-bcp.md)。
