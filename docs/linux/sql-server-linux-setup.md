---
title: Linux 上的 SQL Server 的安装指南
titleSuffix: SQL Server
description: 安装、 更新和卸载 Linux 上的 SQL Server。 本文介绍如何联机、 脱机和无人参与的方案。
author: VanMSFT
ms.author: vanto
manager: jroth
ms.date: 05/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: c4e58111fd6a584344b4f73e6986774040aa6211
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833224"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Linux 上的 SQL Server 的安装指南

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供了有关安装、 更新和卸载 SQL Server 2017 和 Linux 上的 SQL Server 2019 预览版指南。

> [!TIP]
> 本指南 coves 几种部署方案。 如果您仅查找的分步安装说明，跳转到快速入门教程之一：
> - [RHEL 快速入门](quickstart-install-connect-red-hat.md)
> - [SLES 快速入门](quickstart-install-connect-suse.md)
> - [Ubuntu 快速入门](quickstart-install-connect-ubuntu.md)
> - [Docker 快速入门](quickstart-install-connect-docker.md)

有关常见问题的解答，请参阅[SQL Server Linux 常见问题](../linux/sql-server-linux-faq.md)。

## <a id="supportedplatforms"></a> 支持的平台

Red Hat Enterprise Linux (RHEL)、 SUSE Linux Enterprise Server (SLES) 和 Ubuntu 上支持 SQL Server 2017。 它还支持作为 Docker 映像，可以在 Docker 的 Windows/mac。 或在 Linux 上的 Docker 引擎运行

| 平台 | 受支持的版本 | 获取
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [Get RHEL 7.6](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [获取 SLES v12 SP2](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [获取 Ubuntu 16.04](http://releases.ubuntu.com/xenial/)
| **Docker 引擎** | 1.8+ | [获取 Docker](https://www.docker.com/get-started)

Microsoft 还支持部署和使用 OpenShift 和 Kubernetes 来管理 SQL Server 容器。

> [!NOTE]
> SQL Server 经过测试且支持在 Linux 上的前面列出的分发版。 如果您选择不受支持的操作系统上安装 SQL Server，请查看**的支持策略**一部分[Microsoft SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)若要了解支持影响。

## <a id="system"></a> 系统要求

SQL Server 2017 具有以下适用于 Linux 的系统要求：

|||
|-----|-----|
| **内存** | 2 GB |
| **“文件系统”** | **XFS**或**EXT4** (其他文件系统，如**BTRFS**，均不受支持) |
| **磁盘空间** | 6 GB |
| **处理器速度** | 2 GHz |
| **处理器核心** | 2 个核心 |
| **处理器类型** | 仅 x64 兼容 |

如果您使用**网络文件系统 (NFS)** 在生产中，远程共享，请注意以下支持要求：

- 使用 NFS 版本**4.2 或更高版本**。 较旧版本的 NFS 不支持所需的功能，例如 fallocate 和稀疏文件创建，普遍适用于现代文件系统。
- 仅定位 **/var/opt/mssql**上 NFS 装入的目录。 不支持其他文件，如 SQL Server 系统二进制文件。
- 请确保装载的远程共享时，NFS 客户端，使用 nolock 选项。

## <a id="repositories"></a> 配置源存储库

当您安装或升级 SQL Server 时，可从你配置的 Microsoft 存储库获取最新版本的 SQL Server。 快速入门教程使用 SQL Server 2017 累积更新**CU**存储库。 但您可以改为配置**GDR**存储库或**预览版 (vNext)** 存储库。 存储库以及如何配置它们的详细信息，请参阅[Linux 上的 SQL Server 配置存储库](sql-server-linux-change-repo.md)。

## <a id="platforms"></a> 安装 SQL Server 2017

从命令行，可以在 Linux 上安装 SQL Server 2017。 有关分步说明，请参阅以下快速入门：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-docker.md)
- [在 Azure 中预配 SQL VM](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

在安装后，请考虑进行其他配置更改，以获得最佳性能。 有关详细信息，请参阅[的性能最佳实践和 Linux 上的 SQL Server 配置准则](sql-server-linux-performance-best-practices.md)。

## <a id="sqlvnext"></a> 安装 SQL Server 2019 预览版

可以在上一节中使用相同的快速入门链接在 Linux 上安装 SQL Server 2019 预览。 但是，必须注册**预览版 (vNext)** 而不是存储库**CU**存储库。 快速入门教程提供有关如何执行此操作的说明。  

## <a id="upgrade"></a> 更新 SQL Server

若要更新**mssql server**打包到最新版本，请使用以下命令基于你的平台之一：

| 平台 | 包更新命令 |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

这些命令将下载最新的包并替换 /opt/mssql/ 下的`/opt/mssql/`。 用户生成的数据库和系统数据库不受此操作。

> [!TIP]
> 如果您第一[更改配置存储库](sql-server-linux-change-repo.md)，很可能**更新**命令以升级你的 SQL Server 版本。 这是只有的情况下，如果两个存储库之间，支持的升级路径。

## <a id="rollback"></a> 回滚 SQL Server

回滚或降级到以前的版本的 SQL Server，使用以下步骤：

1. 确定想要降级到 SQL Server 包的版本号。 有关包号码的列表，请参阅[发行说明](../linux/sql-server-linux-release-notes.md)。

1. 降级到早期版本的 SQL Server。 在以下命令，将为`<version_number>`使用您在第一步中标识的 SQL Server 版本号。

   | 平台 | 包更新命令 |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> 它仅支持要降级到的相同主版本，如 SQL Server 2017 中的发行版。

## <a id="versioncheck"></a> 检查已安装的 SQL Server 版本

若要验证你的当前版本和版本的 Linux 上的 SQL Server，请使用以下过程：

1. 如果尚未安装，请安装[SQL Server 命令行工具](sql-server-linux-setup-tools.md)。

1. 使用**sqlcmd**运行 TRANSACT-SQL 命令，显示你的 SQL Server 版本和版本。

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> 卸载 SQL Server

若要删除**mssql server**包在 Linux 上，请使用以下命令基于你的平台之一：

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

- 请按照初始步骤中[快速入门](#platforms)注册存储库并安装 SQL Server。
- 在运行时`mssql-conf setup`，将[环境变量](sql-server-linux-configure-environment-variables.md)，并使用`-n`（无提示） 选项。

下面的示例配置与 SQL Server 的 Developer edition **MSSQL_PID**环境变量。 它还会接受 EULA (**ACCEPT_EULA**)，并设置 SA 用户密码 (**MSSQL_SA_PASSWORD**)。 `-n`参数执行进行无提示的安装的配置值存在于环境变量。

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

此外可以创建执行其他操作的脚本。 例如，可以安装其他 SQL Server 包。

有关更详细的示例脚本，请参阅下面的示例：

- [Red Hat 无人参与的安装脚本](sample-unattended-install-redhat.md)
- [SUSE 无人参与的安装脚本](sample-unattended-install-suse.md)
- [Ubuntu 无人参与的安装脚本](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> 脱机安装

如果你的 Linux 计算机无法访问中使用的在线存储库[快速入门](#platforms)，可以直接下载包文件。 这些包位于 Microsoft 存储库， [ https://packages.microsoft.com ](https://packages.microsoft.com)。

> [!TIP]
> 如果使用快速入门中的步骤已成功安装，您不需要下载或手动安装 SQL Server 包。 本部分仅适用于脱机方案。

1. **下载你的平台的数据库引擎包**。 包详细信息部分中找到包下载链接[发行说明](../linux/sql-server-linux-release-notes.md)。

1. **将下载的包移到 Linux 计算机**。 如果使用另一台计算机下载包，将包移到 Linux 计算机的一种方法是使用**scp**命令。

1. **安装数据库引擎包**。 使用以下命令基于你的平台之一。 在此示例包文件的名称替换为你下载的确切名称。

   | 平台 | 包安装命令 |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > 您还可以使用安装 RPM 包 （RHEL 和 SLES）`rpm -ivh`命令，但在上表中的命令会自动安装依赖项如果可从已批准的存储库。

1. **解决缺少的依赖项**:你可能在此时缺少依赖项。 如果没有，可以跳过此步骤。 在 Ubuntu，如果你有权访问已批准存储库包含这些依赖项，最简单的解决方案是使用`apt-get -f install`命令。 此命令还完成了 SQL Server 的安装。 若要手动检查依赖项，请使用以下命令：

   | 平台 | 依赖项列表命令 |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   在解决缺少的依赖项之后, 尝试再次安装 mssql server 包。

1. **完成 SQL Server 安装程序**。 使用**mssql conf**完成 SQL Server 安装程序：

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="licensing-and-pricing"></a>授权和定价

SQL Server 许可适用于 Linux 和 Windows 相同。 详细了解 SQL Server 许可和定价，请参阅[授权的 SQL Server 如何](https://www.microsoft.com/sql-server/sql-server-2017-pricing)。

## <a name="optional-sql-server-features"></a>可选的 SQL Server 功能

安装完成后，您也可以安装，或者启用 SQL Server 的可选功能。

- [SQL Server 命令行工具](sql-server-linux-setup-tools.md)
- [SQL Server 代理](sql-server-linux-setup-sql-agent.md)
- [SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md)
- [机器学习服务 （R、 Python）](sql-server-linux-setup-machine-learning.md)
- [SQL Server Integration Services](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> 有关常见问题的解答，请参阅[SQL Server Linux 常见问题](sql-server-linux-faq.md)。
