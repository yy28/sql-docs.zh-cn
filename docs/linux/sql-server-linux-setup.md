---
title: "在 Linux 上安装 SQL Server 自 2017 年 1 |Microsoft 文档"
description: "安装、 更新和卸载 Linux 上的 SQL Server。 本主题介绍联机、 脱机和无人参与的方案。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/26/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.workload: Active
ms.openlocfilehash: 8d61ba8334d81c46643d15b38173b6b2dd2e1a93
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>在 Linux 上的 SQL Server 安装指南

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主题说明如何安装、 更新和卸载 Linux 上的 SQL Server 2017。 Red Hat Enterprise Linux (RHEL)、 SUSE Linux 企业服务器 (SLES) 和 Ubuntu 支持 SQL Server 自 2017 年。 此外，还可以作为可在 Linux 或 Docker 为 Windows/mac。 上的 Docker 引擎运行的 Docker 映像

> [!TIP]
> 若要快速开始，跳转到快速入门教程： 之一[RHEL](quickstart-install-connect-red-hat.md)， [SLES](quickstart-install-connect-suse.md)， [Ubuntu](quickstart-install-connect-ubuntu.md)，或[Docker](quickstart-install-connect-docker.md)。

## <a id="supportedplatforms"></a>支持的平台

以下 Linux 平台上支持 SQL Server 2017:

| 平台 | 支持的版本 | 获取
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 或 7.4 | [获取 RHEL 7.4](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [获取 SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [获取 Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Docker 引擎** | 1.8+ | [获取 Docker](http://www.docker.com/products/overview)

## <a id="system"></a>系统要求

SQL Server 2017 具有以下适用于 Linux 的系统要求：

|||
|-----|-----|
| **内存** | 3.25 GB |
| **“文件系统”** | **XFS**或**EXT4** (其他文件系统，如**BTRFS**，不支持) |
| **磁盘空间** | 6 GB |
| **处理器速度** | 2 GHz |
| **处理器核心** | 2 核 |
| **处理器类型** | 仅 x64 兼容 |

如果你使用**网络文件系统 (NFS)**在生产中的远程共享，请注意以下支持要求：

- 使用 NFS 版本**4.2 或更高版本**。 NFS 的较旧版本不支持所需的功能，如 fallocate 和稀疏文件创建，普遍适用于现代文件系统。
- 仅查找**/var/opt/mssql**上 NFS 装入的目录。 其他文件，如 SQL Server 系统二进制文件，不支持。
- 确保安装对远程共享时，NFS 客户端，使用 nolock 选项。

## <a id="platforms"></a> 安装 SQL Server

从命令行，可以在 Linux 上安装 SQL Server。 有关说明，请参阅以下快速入门教程之一：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="upgrade"></a>更新 SQL Server

若要更新**mssql server**打包到最新版本，请使用以下命令基于你的平台之一：

| 平台 | 包更新命令 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

这些命令下载最新的包并将位于的二进制文件`/opt/mssql/`。 用户生成的数据库和系统数据库不受此操作。

## <a id="rollback"></a>回滚 SQL Server

回滚或降级到以前的版本的 SQL Server，使用以下步骤：

1. 标识你想要降级到 SQL Server 程序包的版本号。 有关包号码的列表，请参阅[发行说明](sql-server-linux-release-notes.md)。

1. 降级到以前的版本的 SQL Server。 在以下命令，将`<version_number>`与您在第一步中标识的 SQL Server 版本号。

   | 平台 | 包更新命令 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> 它仅支持降级的相同的主版本，如 SQL Server 自 2017 年中的发行版。

## <a id="versioncheck"></a>检查安装的 SQL Server 版本

若要验证你的当前版本和版本的 Linux 上的 SQL Server，请使用以下过程：

1. 如果尚未安装，安装[SQL Server 命令行工具](sql-server-linux-setup-tools.md)。

1. 使用**sqlcmd**运行 TRANSACT-SQL 命令以显示 SQL Server 版本和版本。

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a>卸载 SQL Server

若要删除**mssql server**打包在 Linux 上，请使用以下命令基于你的平台之一：

| 平台 | 包删除命令 |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

删除包不会删除生成的数据库文件。 如果你想要删除的数据库文件，使用以下命令：

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="repositories"></a>配置源存储库

当安装或升级 SQL Server 时，你从你配置的 Microsoft 存储库中获取最新版本的 SQL Server。

### <a name="repository-options"></a>存储库选项

有两种主要类型的每个分布的存储库：

- **累积更新 (CU)**: 累积更新 (CU) 存储库包含自该版本为基的 SQL Server 版本和任何 bug 修复或改进的包。 累积更新是特定于发行版中，如 SQL Server 自 2017 年。 正则的频率发布它们。

- **GDR**: GDR 储存库自该版本中包含的基本 SQL Server 版本和仅关键的修复程序和安全更新的包。 这些更新也会添加到下一步 CU 发行版。

每个 CU 和 GDR 版本包含完整的 SQL Server 程序包和所有以前的更新，该存储库。 从 GDR 版本更新到 CU 版本受更改 SQL Server 配置的存储库。 你还可以[降级](#rollback)到在主要版本中的任何版本 (ex： 自 2017 年)。 更新从 CU 的 GDR 发行版的版本不支持。

### <a name="check-your-configured-repository"></a>检查你配置的存储库

如果你想要验证配置了哪些存储库，使用以下依赖于平台的方法。

| 平台 | 过程 |
|-----|-----|
| RHEL | 1.查看中的文件**/etc/yum.repos.d**目录：`sudo ls /etc/yum.repos.d`<br/>2.查找配置 SQL Server 目录中，如文件**mssql server.repo**。<br/>3.输出文件的内容：`sudo cat /etc/yum.repos.d/mssql-server.repo`<br/>4.**名称**属性是配置的存储库。|
| SLES | 1.运行以下命令：`sudo zypper info mssql-server`<br/>2.**存储库**属性是配置的存储库。 |
| Ubuntu | 1.运行以下命令：`sudo cat /etc/apt/sources.list`<br/>2.检查 mssql 服务器的程序包 URL。 |

存储库 URL 的末尾确认存储库类型：

- **mssql server**： 预览存储库。
- **mssql server 2017**: CU 存储库。
- **mssql server 2017 gdr**: GDR 存储库。

### <a name="change-the-source-repository"></a>更改源存储库

若要配置的 CU 或 GDR 存储库，请使用以下步骤：

> [!NOTE]
> [快速入门教程](#platforms)配置 CU 存储库。 如果你按照这些教程，你不需要使用以下步骤以继续使用 CU 存储库。 这些步骤才需要更改你配置的存储库。

1. 如有必要，删除以前配置的存储库。

   | 平台 | 存储库 | 存储库删除命令 |
   |---|---|---|
   | RHEL | **全部** | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES | **CTP** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | | **CU** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017'` |
   | | **GDR** | `sudo zypper removerepo 'packages-microsoft-com-mssql-server-2017-gdr'`|
   | Ubuntu | **CTP** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` 
   | | **CU** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017 xenial main'` | 
   | | **GDR** | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr xenial main'` |

1. 有关**Ubuntu 仅**，导入公共存储库 GPG 密钥。

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. 配置新的存储库。

   | 平台 | 存储库 | Command |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [安装](#platforms)或[更新](#upgrade)SQL Server 和任何相关包从新的存储库。

   > [!IMPORTANT]
   > 此时，如果你选择使用安装教程之一，如[快速入门教程](#platforms)，请记住您刚配置的目标存储库。 不在本教程中重复该步骤。 这是如果你配置 GDR 存储库，尤其如此，因为快速入门教程使用 CU 存储库。

## <a id="unattended"></a>无人参与的安装

可以按以下方式来执行无人参与的安装：

- 按照初始步骤中[快速入门教程](#platforms)来注册存储库和安装 SQL Server。
- 当你运行`mssql-conf setup`，将其设置[环境变量](sql-server-linux-configure-environment-variables.md)并用`-n`（无提示） 选项。

下面的示例将配置的 SQL Server 的开发人员版**MSSQL_PID**环境变量。 它还会接受 EULA (**ACCEPT_EULA**) 和设置的 SA 用户密码 (**MSSQL_SA_PASSWORD**)。 `-n`参数执行悄悄地的安装其中的配置值从环境变量中提取。

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

你还可以创建执行其他操作的脚本。 例如，你可以安装其他 SQL Server 包。

有关的更详细的示例脚本，请参阅下面的示例：

- [Red Hat 无人参与的安装脚本](sample-unattended-install-redhat.md)
- [SUSE 无人参与的安装脚本](sample-unattended-install-suse.md)
- [Ubuntu 无人参与的安装脚本](sample-unattended-install-ubuntu.md)

## <a id="offline"></a>脱机安装

如果你的 Linux 计算机无访问权限到联机存储库中使用[快速入门](#platforms)，你可以直接下载的包文件。 这些包位于 Microsoft 存储库中，网址为 [https://packages.microsoft.com](https://packages.microsoft.com)。

> [!TIP]
> 如果你成功安装快速入门中的步骤，你不需要下载，或者手动安装以下程序包。 本部分项仅用于脱机方案。

1. **下载你的平台的数据库引擎包**。 包详细信息部分中找到包下载链接[发行说明](sql-server-linux-release-notes.md)。

1. **将下载的包移到你的 Linux 计算机**。 如果一台计算机用于下载的程序包，将包移动到你的 Linux 计算机的一个方法是使用**scp**命令。

1. **安装数据库引擎包**。 使用以下命令基于你的平台之一。 在此示例中的包文件名称替换为你下载的确切名称。

   | 平台 | 包删除命令 |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > 您还可以使用安装 RPM 包 （RHEL 和 SLES）`rpm -ivh`命令，但上表中的命令自动安装依赖项如果可从批准存储库。

1. **解决缺少的依赖关系**： 你可能必须在此点缺失的依赖关系。 如果没有，可以跳过此步骤。 在 Ubuntu，如果您有权访问已批准的存储库包含这些依赖关系，最简单的解决方案是使用`apt-get -f install`命令。 此命令还完成 SQL Server 的安装。 若要手动检查依赖关系，请使用以下命令：

   | 平台 | 依赖项列表命令 |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   在解决了缺少依赖关系之后, 尝试再次安装 mssql server 包。

1. **完成 SQL Server 安装程序**。 使用**mssql conf**若要完成 SQL Server 安装程序：

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="next-steps"></a>后续步骤

安装完成后，你还可以安装其他可选的 SQL Server 包。

- [SQL Server 命令行工具](sql-server-linux-setup-tools.md)
- [SQL Server 代理](sql-server-linux-setup-sql-agent.md)
- [SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services (Ubuntu)](sql-server-linux-setup-ssis.md)

连接到 SQL Server 实例以开始创建和管理数据库。 若要开始，请参阅快速入门教程:

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
