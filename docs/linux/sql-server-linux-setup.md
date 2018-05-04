---
title: 在 Linux 上的 SQL Server 2017 的安装指南 |Microsoft 文档
description: 安装、 更新和卸载 Linux 上的 SQL Server。 本文介绍如何联机、 脱机和无人参与的方案。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/06/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: 2b3b4f6e8214136189cbd004ebd8115670dd2647
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>在 Linux 上的 SQL Server 安装指南

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供有关安装、 更新和卸载 SQL Server 自 2017 年在 Linux 上的指导。

> [!TIP]
> 本指南 coves 几种部署方案。 如果你仅要寻找的分步安装说明，请跳转到快速入门之一：
> - [RHEL 快速入门](quickstart-install-connect-red-hat.md)
> - [SLES 快速入门](quickstart-install-connect-suse.md)
> - [Ubuntu 快速入门](quickstart-install-connect-ubuntu.md)
> - [Docker 快速入门](quickstart-install-connect-docker.md)

有关的常见问题的答案，请参阅[Linux 常见问题的 SQL Server](../linux/sql-server-linux-faq.md)。

## <a id="supportedplatforms"></a> 支持的平台

Red Hat Enterprise Linux (RHEL)、 SUSE Linux 企业服务器 (SLES) 和 Ubuntu 支持 SQL Server 自 2017 年。 它还支持作为可在 Linux 或 Docker 为 Windows/mac。 上的 Docker 引擎运行的 Docker 映像

| 平台 | 支持的版本 | 获取
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 或 7.4 | [获取 RHEL 7.4](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [获取 SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [获取 Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Docker 引擎** | 1.8+ | [获取 Docker](http://www.docker.com/products/overview)

Microsoft 还支持部署和管理 SQL Server 容器通过 OpenShift 和 Kubernetes。

> [!NOTE]
> SQL Server 经过测试且在 Linux 上支持的前面列出的分发版。 如果你选择的不受支持的操作系统上安装 SQL Server，请查看**支持策略**部分[Microsoft SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)以了解支持影响。

## <a id="system"></a> 系统要求

SQL Server 2017 具有以下适用于 Linux 的系统要求：

|||
|-----|-----|
| **内存** | 2 GB |
| **文件系统** | **XFS**或**EXT4** (其他文件系统，如**BTRFS**，不支持) |
| **磁盘空间** | 6 GB |
| **处理器速度** | 2 GHz |
| **处理器核心** | 2 核 |
| **处理器类型** | 仅 x64 兼容 |

如果你使用**网络文件系统 (NFS)** 在生产中的远程共享，请注意以下支持要求：

- 使用 NFS 版本**4.2 或更高版本**。 NFS 的较旧版本不支持所需的功能，如 fallocate 和稀疏文件创建，普遍适用于现代文件系统。
- 仅查找 **/var/opt/mssql**上 NFS 装入的目录。 其他文件，如 SQL Server 系统二进制文件，不支持。
- 确保安装对远程共享时，NFS 客户端，使用 nolock 选项。

## <a id="repositories"></a> 配置源存储库

当安装或升级 SQL Server 时，你从你配置的 Microsoft 存储库中获取最新版本的 SQL Server 自 2017 年。 快速入门使用**累积更新 (CU)** 存储库。 但是可以改为配置**GDR**存储库。 存储库以及如何配置它们的详细信息，请参阅[为在 Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

> [!IMPORTANT]
> 如果你以前安装的 CTP 或 RC 版本的 SQL Server 自 2017 年，你必须删除预览存储库并注册一个常规正式版 (GA)。 有关详细信息，请参阅[为在 Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

## <a id="platforms"></a> 安装 SQL Server

从命令行，可以在 Linux 上安装 SQL Server。 有关说明，请参阅以下快速入门之一：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="upgrade"></a> 更新 SQL Server

若要更新**mssql server**打包到最新版本，请使用以下命令基于你的平台之一：

| 平台 | 包更新命令 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

这些命令下载最新的包并将位于的二进制文件`/opt/mssql/`。 用户生成的数据库和系统数据库不受此操作。

## <a id="rollback"></a> 回滚 SQL Server

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

## <a id="versioncheck"></a> 检查安装的 SQL Server 版本

若要验证你的当前版本和版本的 Linux 上的 SQL Server，请使用以下过程：

1. 如果尚未安装，安装[SQL Server 命令行工具](sql-server-linux-setup-tools.md)。

1. 使用**sqlcmd**运行 TRANSACT-SQL 命令以显示 SQL Server 版本和版本。

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> 卸载 SQL Server

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

## <a id="unattended"></a> 无人参与的安装

可以按以下方式来执行无人参与的安装：

- 按照初始步骤中[快速入门](#platforms)来注册存储库和安装 SQL Server。
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

## <a id="offline"></a> 脱机安装

如果你的 Linux 计算机无访问权限到联机存储库中使用[快速入门](#platforms)，你可以直接下载的包文件。 这些包位于 Microsoft 存储库， [ https://packages.microsoft.com ](https://packages.microsoft.com)。

> [!TIP]
> 如果你成功安装快速入门中的步骤，你不需要下载，或者手动安装 SQL Server 程序包。 本部分项仅用于脱机方案。

1. **下载你的平台的数据库引擎包**。 包详细信息部分中找到包下载链接[发行说明](sql-server-linux-release-notes.md)。

1. **将下载的包移到你的 Linux 计算机**。 如果一台计算机用于下载的程序包，将包移动到你的 Linux 计算机的一个方法是使用**scp**命令。

1. **安装数据库引擎包**。 使用以下命令基于你的平台之一。 在此示例中的包文件名称替换为你下载的确切名称。

   | 平台 | 包安装命令 |
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

## <a name="optional-sql-server-features"></a>可选的 SQL Server 功能

安装完成后，也可以安装或启用可选的 SQL Server 功能。

- [SQL Server 命令行工具](sql-server-linux-setup-tools.md)
- [SQL Server 代理](sql-server-linux-setup-sql-agent.md)
- [SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md)
- [SQL Server Integration Services (Ubuntu)](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> 有关的常见问题的答案，请参阅[Linux 常见问题的 SQL Server](sql-server-linux-faq.md)。
