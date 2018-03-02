---
title: "SQL Server on Linux 常见问题 |Microsoft 文档"
description: "这篇文章提供了在 Linux 上运行的 SQL Server 相关的常见问题的答案。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/22/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Active
ms.openlocfilehash: 3fad3fb2892e5a91e42eefb5f00932c39d00064f
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/24/2018
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>在 Linux 上的 SQL Server 常见问题 (FAQ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下部分提供常见的问题和答案的 SQL Server 在 Linux 上运行。

## <a name="general-questions"></a>一般问题

1. **支持哪些 Linux 平台？**

   Red Hat Enterprise Server、 SUSE Linux 企业服务器和 Ubuntu 上当前支持 SQL Server。 它还可以运行在使用 Docker 容器中。 有关受支持版本的最新信息，请参阅[受支持的平台](sql-server-linux-setup.md#supportedplatforms)。

1. **将在其他平台上的 Linux 上的 SQL Server 工作**？

   你可能可以安装和 Linux 的其他发行版上运行 SQL Server。 例如，CentOS 是与紧密相关 Red Hat Enterprise Server，因此你可能能够安装 RPM SQL Server 包。 这可能是适用于其他密切相关的分布。 主要问题是测试和支持。 SQL Server 仅已测试，并且在 Red Hat Enterprise Linux、 SUSE Linux 企业服务器和 Ubuntu 上才支持。

1. **在 Linux 上支持哪些 SQL Server 功能？**

   有关支持的功能和已知的问题的完整列表，请参阅[发行说明](sql-server-linux-release-notes.md)。

1. **SQL Server 支持策略是什么？**

   若要了解支持策略，查看[SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

1. **我将来自 Windows SQL Server 背景。有资源来帮助您了解如何在 Linux 上使用 SQL Server 吗？**

   [快速入门](sql-server-linux-setup.md#platforms)提供有关如何在 Linux 上安装 SQL Server 和运行 TRANSACT-SQL 查询的分步说明。 其他教程提供了有关在 Linux 上使用 SQL Server 的其他说明。 提示的第三方列表，请参阅[MSSQLTIPS 列表的 SQL Server 上 Linux 提示](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)。

## <a name="installation"></a>安装

1. **如何获取我的 Linux 服务器上安装的 SQL Server？**

   Microsoft 维护安装 SQL Server 的包存储库，并支持通过 yum，zypper，如的本机包管理器的安装以及公寓。 若要快速安装，请参阅之一[快速入门](sql-server-linux-setup.md#platforms)。

1. **可以在 Linux 子系统适用于 Windows 10 上安装 SQL Server？**

   否。 在 Windows 10 上运行的 Linux 目前不受支持的平台 SQL Server 和相关的工具。

1. **SQL Server 2017 对于数据文件可以使用哪些 Linux 文件系统？**

   当前在 Linux 上的 SQL Server 支持 ext4 和 XFS。 根据需要在将来，将添加对其他文件系统支持。

1. **可以下载脱机安装 SQL Server 的安装程序包？**

   是。 有关详细信息，请参阅下载中的链接的包[发行说明](sql-server-linux-release-notes.md)。 此外，请查看[对于脱机安装说明](sql-server-linux-setup.md#offline)。

1. **可以在 Linux 上执行无人参与的安装的 SQL Server？**

   是。 有关无人参与安装的讨论，请参阅[在 Linux 上的 SQL Server 安装指南](sql-server-linux-setup.md#unattended)。 请参阅的示例脚本[Red Hat](sample-unattended-install-redhat.md)， [SUSE Linux Enterprise Server](sample-unattended-install-suse.md)，和[Ubuntu](sample-unattended-install-ubuntu.md)。 此外可以查看[此示例脚本](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/)由 SQL Server 客户咨询团队创建。

## <a name="tools"></a>工具

1. **可以用于 SQL Server Management Studio 客户端在 Windows 上访问在 Linux 上的 SQL Server？**

   是，你可以使用所有你在访问在 Linux 上的 SQL Server 的 Windows 运行的现有工具。 其中包括从 Microsoft SQL Server Management Studio (SSMS)、 SQL Server Data Tools (SSDT) 和 OSS 等工具和第三方工具。

1. **是否有运行在 Linux 的 SSMS 之类的工具？**

   新的 Microsoft SQL 操作 Studio （预览版） 是用于管理 SQL Server 的跨平台工具。 有关详细信息，请参阅[什么是 Microsoft SQL 操作 Studio （预览版）](../sql-operations-studio/what-is.md)。

1. **如 sqlcmd 和 bcp 命令是否可在 Linux 上？**

   是， [sqlcmd 和 bcp](sql-server-linux-setup-tools.md)本机 Linux、 macOS 和 Windows 上可用。 此外，使用新[mssql 脚本编写器](https://github.com/Microsoft/mssql-scripter)上 Linux、 macOS，或 Windows 生成 SQL 数据库运行任何位置的 T-SQL 脚本的命令行工具。 另请参阅发布为预览[mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。

1. **可以查看活动监视器的实例通过 Windows 上的 SSMS 连接时它正在运行在 Linux 上？**

   是，可以使用在 Windows 上的 SSMS 远程连接，并使用工具 / 功能如作为活动监视器上的 Linux 实例的命令。

1. **可用于监视在 Linux 上的 SQL Server 性能工具有哪些？**

   你可以使用[系统动态管理视图 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)来收集有关 SQL Server，包括 Linux 进程信息的信息的各种类型。 你可以使用[Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)以提高查询性能。 其他工具，如内置[性能仪表板](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)、 远程在 SQL Server Management Studio (SSMS) 在 Windows 中工作。

## <a name="administration"></a>管理

1. **Microsoft 已经如 SQL Server 配置管理器中的应用程序在 Linux 上？**

   是的是用于在 Linux 上的 SQL Server 的配置工具： [mssql conf](sql-server-linux-configure-mssql-conf.md)。

1. **在 Linux 上的 SQL Server 支持多个实例在同一主机上？**

   我们建议在拥有多个不同实例的主机上运行多个容器。 需要在不同的端口上侦听的每个容器。 有关详细信息，请参阅[运行多个 SQL Server 容器](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers)。

1. **在 Linux 上支持 Active Directory 身份验证？**

   是。 有关详细信息，请参阅[与在 Linux 上的 SQL Server 的 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。

1. **始终位于和群集在 Linux 中受支持？**

   在 Linux 上的 Pacemaker 可以获得故障转移群集和 Linux 上的高可用性。 有关详细信息，请参阅[业务连续性和数据库恢复-在 Linux 上的 SQL Server](sql-server-linux-business-continuity-dr.md)。

1. **是否可以将复制从 Linux 到 Windows，反之亦然配置？**

   读取扩展副本可以用于 Windows 和 Linux 之间单向数据复制。

1. **是否可以从 Windows 的较旧版本的 SQL Server 中现有数据库迁移到 Linux？**

   是，有[几种方法](sql-server-linux-migrate-overview.md)实现此目的。

1. **是否可以迁移我的数据从 Oracle 和其他数据库引擎，到在 Linux 上的 SQL Server？**

   是。 SSMA 支持从数据库引擎的多种类型的迁移： Microsoft Access、 DB2、 MySQL、 Oracle 和 SAP ASE (以前称为 SAP Sybase ASE)。 有关如何使用 SSMA 的示例，请参阅[将 Oracle 架构迁移到使用 SQL Server Migration Assistant Linux 上的 SQL Server 2017](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)。

1. **SQL Server 文件需要哪些权限？**

   中的所有文件`/var/opt/mssql`文件文件夹应归**mssql**用户，并且属于**mssql**组。 这两个**mssql**用户和组应具有的所有文件和目录的读写权限。 请注意以下特殊方案涉及文件和目录权限：

   * 所需的用来存储 SQL Server 文件的已装入的网络共享 mssql 所有者和组的权限。
   * 如果您在非默认的目录中找到数据库文件或备份，还必须设置该目录的权限。
   * 如果从 0022 更改默认根 umask，则 SQL Server 配置之后安装失败。 然后必须手动向 SQL Server 启动帐户中应用所需的权限。

1. **可以将 SQL Server 文件和目录的所有权更改已安装的 mssql 帐户和组中？**

   我们不支持从默认安装中更改 SQL Server 目录和文件的所有权。 Mssql 帐户和组专门用于 SQL Server，并且没有交互式登录访问权限。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]