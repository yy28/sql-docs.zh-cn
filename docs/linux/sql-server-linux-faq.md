---
title: SQL Server on Linux 常见问题 |Microsoft Docs
description: 本文提供有关 SQL Server 常见问题的解答在 Linux 上运行。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/25/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: c45203e8524fe2df9301250afd1bef40df37bc3d
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419352"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Linux 上的 SQL Server 方面的常见问题 (FAQ)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

以下部分提供常见问题和解答有关 SQL Server Linux 上运行。

## <a name="general-questions"></a>一般问题

1. **支持的 Linux 平台？**

   Red Hat Enterprise Server、 SUSE Linux Enterprise Server 和 Ubuntu 上目前支持 SQL Server。 它还支持使用 Docker 容器中运行。 有关受支持版本的最新信息，请参阅[受支持的平台](sql-server-linux-setup.md#supportedplatforms)。

1. **将在其他平台上的 Linux 上的 SQL Server 工作**？

   SQL Server 经过测试且支持在 Linux 上的前面列出的分发版。 其他 Linux 发行版密切相关，可能能够在运行 SQL Server （例如，CentOS 密切相关到 Red Hat Enterprise Server）。 但如果您选择不受支持的操作系统上安装 SQL Server，请查看**的支持策略**一部分[Microsoft SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)若要了解支持影响。 另请注意，一些社区维护的 Linux 分发没有正式的方法，才能获得支持，如果基础操作系统是问题。

1. **Linux 上的许可工作原理？**

   SQL Server 是获得相同的方式许可适用于 Windows 和 Linux。 事实上，SQL Server 的许可，然后选择要在所选的平台上使用该许可证。 有关详细信息，请参阅[授权的 SQL Server 如何](https://www.microsoft.com/sql-server/sql-server-2017-pricing)。

1. **Linux 上的 SQL Server 是与 Windows 上相同？**

   与在 Windows，SQL Server 数据库引擎的核心都是在 Linux 上相同的。 但是，某些功能当前不支持在 Linux 上。 Linux 不支持的功能的列表，请参阅[不受支持的功能和服务](sql-server-linux-release-notes.md#Unsupported)。 此外查看[已知问题](sql-server-linux-release-notes.md#known-issues)。 在这些列表中指定，除非其他 SQL Server 功能和服务支持在 Linux 上。

1. **SQL Server 的支持策略是什么？**

   若要了解支持策略，请查看[SQL Server 的技术支持策略](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server)。

1. **我来自 Windows SQL Server 背景。是否有资源，以帮助了解如何在 Linux 上使用 SQL Server？**

   [快速入门](sql-server-linux-setup.md#platforms)提供有关如何在 Linux 上安装 SQL Server 并运行 Transact SQL 查询的分步说明。 其他教程提供了有关在 Linux 上使用 SQL Server 的其他说明。 第三方技巧的列表，请参阅[MSSQLTIPS 列表上 Linux 的提示的 SQL Server](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/)。

## <a name="installation"></a>安装

1. **如何获取我的 Linux 服务器上安装 SQL Server？**

   Microsoft 维护安装 SQL Server 的包存储库，支持通过 yum，zypper，如本机包管理器进行安装和 apt。 若要快速安装，请参阅之一[快速入门](sql-server-linux-setup.md#platforms)。

1. **可以在 Linux 子系统适用于 Windows 10 上安装 SQL Server？**

   否。 在 Windows 10 上运行的 Linux 目前不支持的 SQL Server 和相关的工具的平台。

1. **SQL Server 数据文件可以使用哪些 Linux 文件系统？**

   目前在 Linux 上的 SQL Server 支持 ext4 和 XFS。 根据需要在将来，将添加对其他文件系统支持。

1. **可以下载脱机安装 SQL Server 的安装包？**

   是。 有关详细信息，请参阅下载中的链接的包[发行说明](sql-server-linux-release-notes.md)。 此外，请查看[脱机安装说明](sql-server-linux-setup.md#offline)。

1. **可以在 Linux 上执行无人参与的安装的 SQL Server？**

   是。 有关无人参与安装的讨论，请参阅[Linux 上的 SQL Server 的安装指南](sql-server-linux-setup.md#unattended)。 请参阅有关示例脚本[Red Hat](sample-unattended-install-redhat.md)， [SUSE Linux Enterprise Server](sample-unattended-install-suse.md)，并[Ubuntu](sample-unattended-install-ubuntu.md)。 此外可以查看[此示例脚本](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/)创建的 SQL Server 客户顾问团队。

1. **我已购买时应该选择什么版本的 SQL Server？**

   运行 mssql conf 安装程序时为您提供这些选项：  
   `Choose an edition of SQL Server:` <br>
`     1. Evaluation (free, no production use rights, 180-day limit)` <br>
`     2. Developer (free, no production use rights)` <br>
`     3. Express (free)` <br>
`     4. Web (PAID)` <br>
`     5. Standard (PAID)` <br>
`     6. Enterprise (PAID)` <br>
`     7. Enterprise Core (PAID)` <br>
`     8. I bought a license through a retail sales channel and have a product key to enter.`
     
   如果你获取你通过批量许可企业协议的一部分或您的 MSDN 订阅的许可证，你需要选择 4 到 7。 如果你已购买标准版通过零售渠道，您需要选择 8。 


## <a name="tools"></a>工具

1. **可以使用 SQL Server Management Studio 客户端在 Windows 上访问 Linux 上的 SQL Server？**

   是的可以使用 Windows 访问 Linux 上的 SQL Server 上运行的所有现有工具。 其中包括 SQL Server Management Studio (SSMS)、 SQL Server Data Tools (SSDT) 和 OSS 等 Microsoft 工具和第三方工具。

1. **是否有在 Linux 运行的 SSMS 之类的工具？**

   新的 Azure Data Studio （预览版） 是用于管理 SQL Server 的跨平台工具。 有关详细信息，请参阅[什么是 Azure Data Studio （预览版）](../azure-data-studio/what-is.md)。

1. **Sqlcmd 和 bcp 等命令是否可在 Linux 上？**

   是的[sqlcmd 和 bcp](sql-server-linux-setup-tools.md) Linux、 macOS 和 Windows 上本机可用。 此外，使用新[mssql 脚本专家](https://github.com/Microsoft/mssql-scripter)在 Linux、 macOS 或 Windows 生成的任何位置运行的 SQL 数据库的 T-SQL 脚本的命令行工具。 此外，请参阅 preview release [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/)。

1. **它可以查看活动监视器的实例通过 Windows 上的 SSMS 连接时是否运行在 Linux 上？**

   是的可以在 Windows 上使用 SSMS 来远程连接，并使用工具 / 等功能的 Linux 实例上的活动监视器命令。

1. **哪些工具是可用于监视 Linux 上的 SQL Server 性能？**

   可以使用[系统动态管理视图 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)收集各种类型的 SQL Server，包括 Linux 进程信息有关的信息。 可以使用[Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)以提高查询性能。 其他工具，如内置[性能仪表板](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)、 远程中 SQL Server Management Studio (SSMS) 从 Windows 工作。

   > [!TIP]
   > 若要提高性能的一种方法是正确配置 Linux 操作系统和 SQL Server 需。 有关详细信息，请参阅[的性能最佳实践和 Linux 上的 SQL Server 配置准则](sql-server-linux-performance-best-practices.md)。

## <a name="administration"></a>管理

1. **Microsoft 中有创建 Linux 应用等 SQL Server 配置管理器？**

   是的是用于在 Linux 上的 SQL Server 的配置工具： [mssql conf](sql-server-linux-configure-mssql-conf.md)。

1. **Linux 上的 SQL Server 支持多个实例在同一主机上？**

   我们建议要有多个不同实例的主机上运行多个容器。 这很容易实现使用 docker，但需要在不同端口上侦听每个容器。 有关详细信息，请参阅[运行多个 SQL Server 容器](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers)。

1. **在 Linux 上支持 Active Directory 身份验证？**

   是。 有关详细信息，请参阅[使用 Linux 上的 SQL Server 的 Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。

1. **Always On 是，在 Linux 中支持群集功能？**

   使用 Linux 上的 Pacemaker 实现故障转移群集和 Linux 上的高可用性。 有关详细信息，请参阅[业务连续性和数据库恢复-Linux 上的 SQL Server](sql-server-linux-business-continuity-dr.md)。

1. **是否可以配置从 Linux 到 Windows，反之亦然复制？**

   读取缩放副本可以用于 Windows 和 Linux 之间单向数据复制。

1. **是否可以将较旧版本的 SQL Server 中的现有数据库从 Windows 迁移到 Linux？**

   是的还有[几种方法](sql-server-linux-migrate-overview.md)实现此目的。

1. **是否可以迁移我的数据从 Oracle 和其他数据库引擎到 Linux 上的 SQL Server？**

   是。 SSMA 支持将从数据库引擎的几种类型的迁移： Microsoft Access、 DB2、 MySQL、 Oracle 和 SAP ASE (以前称为 SAP Sybase ASE)。 有关如何使用 SSMA 的示例，请参阅[将 Oracle 架构迁移到 SQL Server Linux 上使用 SQL Server Migration Assistant](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json)。

1. **SQL Server 文件需要哪些权限？**

   中的所有文件`/var/opt/mssql`文件夹应归**mssql**用户，并且属于**mssql**组。 这两个**mssql**用户和组应具有的所有文件和目录的读写权限。 请注意以下特殊方案涉及文件和目录的权限：

   * 所需的用于存储 SQL Server 文件的已装载的网络共享 mssql 所有者和组权限。
   * 如果非默认目录中找到数据库文件或备份，则还必须设置该目录的权限。
   * 如果从 0022 更改默认根 umask，SQL Server 配置后安装失败。 然后必须手动向 SQL Server 启动帐户中应用所需的权限。

1. **可以从已安装的 mssql 帐户和组更改 SQL Server 文件和目录的所有权？**

   我们不支持从默认安装中更改 SQL Server 目录和文件的所有权。 Mssql 帐户和组专门用于 SQL Server，并且没有交互式登录访问权限。

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
