---
title: 在 Linux 上安装 SQL Server 命令行工具
titleSuffix: SQL Server
description: 本文介绍如何在 Linux 上安装 SQL Server 工具。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 06/07/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: eff8e226-185f-46d4-a3e3-e18b7a439e63
ms.openlocfilehash: 9b93530b54f2f51f2c00b9d651fcae970507a4cf
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834664"
---
# <a name="install-sqlcmd-and-bcp-the-sql-server-command-line-tools-on-linux"></a>在 Linux 上安装 sqlcmd 和 bcp SQL Server 命令行工具

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

通过下列步骤安装命令行工具、Microsoft ODBC 驱动程序及其依赖项。 **Mssql 工具**包包含：

- **sqlcmd**:命令行查询实用程序。
- **bcp**:大容量导入导出实用程序。

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

1. 运行以下命令以安装 **mssql-tools** 和 unixODBC 开发人员包。

   ```bash
   sudo yum install mssql-tools unixODBC-devel
   ```

   > [!Note] 
   > 若要更新到最新版**mssql 工具**运行以下命令：
   >    ```bash
   >   sudo yum check-update
   >   sudo yum update mssql-tools
   >   ```

1. **可选**:添加`/opt/mssql-tools/bin/`为你**路径**bash shell 中的环境变量。

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

1. **可选**:添加`/opt/mssql-tools/bin/`为你**路径**bash shell 中的环境变量。

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

1. **可选**:添加`/opt/mssql-tools/bin/`为你**路径**bash shell 中的环境变量。

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
brew install mssql-tools
#for silent install: 
#HOMEBREW_NO_ENV_FILTERING=1 ACCEPT_EULA=y brew install mssql-tools
```

## <a id="docker"></a> Docker

Docker 映像中包含 SQL Server 命令行工具。 如果使用交互式命令提示符附加至此映像，则可在本地运行工具。

## <a name="offline-installation"></a>脱机安装

[!INCLUDE[SQL Server Linux offline package installation](../includes/sql-server-linux-offline-package-install-intro.md)]

1. 首先，找到并复制**mssql 工具**Linux 分发包：

   | Linux 分发版 | **mssql 工具**包位置 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/mssql-tools) |

1. 此外找到并复制**msodbcsql**包，这是一个依赖项。 **Msodbcsql**包也上具有依赖项**unixODBC 开发**（Red Hat 和 SLES） 或**unixodbc 开发人员**(Ubuntu)。 位置**msodbcsql**下表中列出的包：

   | Linux 分发版 | ODBC 包位置 |
   |---|---|
   | Red Hat | [https://packages.microsoft.com/rhel/7.3/prod](https://packages.microsoft.com/rhel/7.3/prod) |
   | SLES | [https://packages.microsoft.com/sles/12/prod](https://packages.microsoft.com/sles/12/prod)|
   | Ubuntu 16.04 | [**msodbcsql**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/m/msodbcsql)<br/>[**unixodbc-dev**](https://packages.microsoft.com/ubuntu/16.04/prod/pool/main/u/unixodbc/) |

1. **将下载的包移到 Linux 计算机**。 如果使用另一台计算机下载包，将包移到 Linux 计算机的一种方法是使用**scp**命令。

1. **安装和包**:安装**mssql 工具**并**msodbc**包。 如果遇到任何依赖关系错误，请忽略，直到出现下一步操作。

    | 平台 | 包安装命令 |
    |-----|-----|
    | Red Hat | `sudo yum localinstall msodbcsql-<version>.rpm`<br/>`sudo yum localinstall mssql-tools-<version>.rpm` |
    | SLES | `sudo zypper install msodbcsql-<version>.rpm`<br/>`sudo zypper install mssql-tools-<version>.rpm` |
    | Ubuntu | `sudo dpkg -i msodbcsql_<version>.deb`<br/>`sudo dpkg -i mssql-tools_<version>.deb` |

1. **解决缺少的依赖项**:你可能在此时缺少依赖项。 如果没有，可以跳过此步骤。 在某些情况下，必须手动查找并安装这些依赖项。

    对于 RPM 包，可通过下列命令检查必需的依赖项：

    ```bash
    rpm -qpR msodbcsql-<version>.rpm
    rpm -qpR mssql-tools-<version>.rpm
    ```

    对于 Debian 包，如果你有权访问已批准存储库包含这些依赖项，最简单的解决方案是使用**apt get**命令：

    ```bash
    sudo apt-get -f install
    ```

    > [!NOTE]
    > 使用命令还会完成 SQL Server 包的安装。

    如果此操作对 Debian 包不起作用，可通过下列命令检查必需的依赖项：

    ```bash
    dpkg -I msodbcsql_<version>_amd64.deb | grep "Depends:"
    dpkg -I mssql-tools_<version>_amd64.deb | grep "Depends:"
    ```

## <a name="next-steps"></a>后续步骤

有关如何使用的示例**sqlcmd**若要连接到 SQL Server 并创建一个数据库，请参阅以下快速入门：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)

有关如何使用的示例**bcp**大容量导入和导出数据，请参阅[大容量数据复制到 Linux 上的 SQL Server](sql-server-linux-migrate-bcp.md)。
