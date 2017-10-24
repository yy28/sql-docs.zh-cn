---
title: "在 Linux 上的 SQL Server 自 2017 年 1 的新增功能 |Microsoft 文档"
description: "本主题重点介绍当前版本的 SQL Server 自 2017 年在 Linux 上的新增功能。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: f76985a8721e154269b36b0bdcb40a83f6136cb3
ms.contentlocale: zh-cn
ms.lasthandoff: 10/20/2017

---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Linux 版 SQL Server 2017 的新增功能

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主题介绍在 Linux 上运行的 SQL Server 2017 的新增功能。

## <a name="ga"></a>GA

常规 Availaiblity (GA) 版本包含以下改进和修补程序：

- 现在可以在 NFS 上承载数据库文件。 这会修复问题 NFS 共享磁盘方案，装载远程存储对于容器平台，并为用于 Windows 的 Docker 装载文件夹。
- 其他其他大量 bug 修复和改进。

## <a name="rc2"></a>RC2

RC2 版本包含其他大量 bug 修复和改进。

## <a name="rc1"></a>RC1

RC1 版本包含以下改进和修补程序：

- 对于加密连接启用透明层安全 (TLS)。 有关详细信息，请参阅[Encrypting connections to Linux 上的 SQL Server 连接](sql-server-linux-encrypted-connections.md)。
- 启用[Active Directory 身份验证](sql-server-linux-active-directory-authentication.md)。
- 启用[DB 邮件](../relational-databases/database-mail/database-mail.md)。
- 添加了 IPV6 的支持。
- 初始的 SQL Server 安装程序的添加的环境变量。 有关详细信息，请参阅[与环境变量在 Linux 上配置 SQL Server 设置](sql-server-linux-configure-environment-variables.md)。
- 删除**sqlpackage**从安装二进制文件。 SqlPackage 可以仍然针对 Linux 远程运行从 Windows。
- 共享磁盘群集资源代理集资源的名称，例如它未在 Windows SQL Server 故障转移群集实例。 `@@ServerName`返回的 SQL Server 共享的磁盘群集资源名称;在 RC1 之前它将返回拥有的资源的群集节点的名称。

## <a name="ctp-21"></a>CTP 2.1

CTP 2.1 版本包含以下改进和修补程序：

- 添加[环境变量以配置 SQL Server 服务](sql-server-linux-configure-environment-variables.md)。
- [mssql conf](sql-server-linux-configure-mssql-conf.md)现在需要设置两部分命名约定。
- [Mssql 脚本编写器](https://github.com/Microsoft/sql-xplat-cli)工具。 使用此实用工具，开发人员、 Dba 和 sysadmin，以生成`CREATE`和`INSERT`从 SQL Server、 Azure SQL DB 和 Azure SQL DW 数据库从命令行中的数据库对象的 TRANSACT-SQL 脚本。
- [DBFS 工具](https://github.com/Microsoft/dbfs)。 这是一个开放源代码的工具，通过公开 SQL Server 动态管理视图 (DMV) 中的实时数据，以作为 Linux 操作系统上虚拟目录中的虚拟文件，使 DBA 和 系统管理员可以更轻松地监视 SQL Server。
- SQL Server Integration Services (SSIS) 现在在 Linux 上运行。 此外，没有允许您从命令行在 Linux 上运行 SSIS 包的新包。 有关详细信息，请参阅[博客文章宣布推出适用于 Linux 的 SSIS 支持](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。 借助 Linux CTP 2.1 刷新的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

## <a name="ctp-20"></a>CTP 2.0

CTP 2.0 版本包含以下改进和修补程序：

- 添加**日志传送**SQL Server 代理的功能。
- 已本地化 mssql-conf 的消息。
- 现在 Linux 路径格式在整个 SQL Server 引擎中都兼容。 但支持"c:\\"带前缀的路径将继续。
- 启用 DMV **sys.dm_os_file_exists**。
- 启用 DMV **sys.fn_trace_gettable**。
- 添加[CLR 严格的安全模式](/sql/database-engine/configure-windows/clr-strict-security)。
- SQL 图形。
- 可恢复的联机索引重新生成。
- 自适应查询处理。
- 添加了用于日志文件等系统文件的 UTF-8 编码。
- 修复了内存中数据库位置限制。 
- 添加新的群集类型`CLUSTER_TYPE = EXTERNAL`配置高可用性的可用性组。
- 修复了可用性组侦听程序以进行只读路由。
- 对早期采用计划 (EAP) 客户的生产支持。 注册[此处](http://aka.ms/eapsignup)。

## <a name="ctp-14"></a>CTP 1.4

CTP 1.4 版本包含以下改进和修补程序：

- 启用[SQL Server 代理](sql-server-linux-setup-sql-agent.md)。
  - 启用了 T-SQL 作业功能。
- 修复了时区 Bug：
  - 对亚洲/加尔各答时区的支持。
  - 修复了 GETDATE() 函数。
- 网络异步 I/0 改进：
  - 显著提高了内存中 OLTP 工作负荷性能。
- Docker 映像现在包括 SQL Server 命令行实用程序。 (sqlcmd/bcp)。
- 启用了备份的虚拟设备接口 (VDI) 支持。
- 现在可以安装使用之后修改的 TempDB 位置`ALTER DATABASE`。

## <a name="ctp-13"></a>CTP 1.3

CTP 1.3 版本包含以下改进和修补程序：

- 启用[的全文搜索](sql-server-linux-setup-full-text-search.md)功能。
- 启用 Always On[可用性组功能](sql-server-linux-availability-group-overview.md)以实现高可用性。
- 中的其他功能**mssql conf**:
  - 第一个时间设置使用**mssql conf**。 请参阅中的 mssql conf 利用[安装指南](sql-server-linux-setup.md#platforms)。
  - 启用可用性组。 请参阅[可用性组主题](sql-server-linux-availability-group-overview.md)。
- 修复了对内存中 OLTP 文件组的本机 Linux 路径支持。
- 启用了 dm_os_host_info DMV 功能。

## <a name="ctp-12"></a>CTP 1.2

CTP 1.2 版本包含以下改进和修补程序：

- 支持[SUSE Linux Enterprise Server v12 SP2](quickstart-install-connect-suse.md)。
- 核心引擎和稳定性改进的 bug 修复。
- Docker 映像： 
  - 固定[第 1 个问题](https://github.com/Microsoft/mssql-docker/issues/1)通过将 Python 添加到映像。
  - 删除`/opt/mssql/data`作为默认卷。
- 已更新至 .NET 4.6.2。

## <a name="ctp-11"></a>CTP 1.1

CTP 1.1 版本包含以下改进和修补程序：

- 对 Red Hat Enterprise Linux 版本 7.3 的支持。
- 对 Ubuntu 16.10 的支持。
- 已将 Docker OS 层升级至 Ubuntu 16.04。
- 修复了 Docker 映像中的遥测问题。
- 修复了 SQL Server 安装脚本的相关 Bug。
- 增强了本机编译的 T-SQL 模块的性能，包括：
  - **OPENJSON**， **FOR JSON**， **JSON**内置。
  - 计算列（仅在持久化计算列上仅允许进行索引，而不是在内存中表的非持久化计算列上）。
  - **跨应用**操作。
- 新语言功能：
  - 字符串函数： **TRIM**， **CONCAT_WS**，**翻译**和**STRING_AGG**支持**WITHIN GROUP (ORDER BY)**。
  - **大容量导入**现在支持 CSV 格式和 Azure Blob 存储作为文件源。

在兼容性模式 140 下：

- 当行是在增量存储中，改进了更新到这种情况中的非聚集列存储索引的性能。 从删除和插入操作改为了更新。 还将使用的计划形状从宽改为窄。
- 批处理模式查询现在支持"内存授予反馈循环"。 这将提高运行使用批处理模式的重复查询的系统上的并发度和吞吐量。 这可以使更多的查询能够在启动查询前阻止内存的其他系统上运行。
- 在批处理模式并行通过忽略批处理模式计划，以便并行计划，以针对 columnstores 改为选择的普通计划中的改进的性能。 

[从 Service Pack 1 的改进](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)此 CTP1.1 版本中：
- 克隆为 CLR，Filestream/Filetable，内存中和查询存储对象的数据库。
  - **更新 10/18/2017年**： 时进一步测试，Filestream 目前不支持在 Linux 上的 SQL Server 2017 GA 版本  
- **创建**或**ALTER**可编程性对象的运算符。
- 新**使用提示**查询选项的查询处理器中提供提示。 此处详细了解：[查询提示](../t-sql/queries/hints-transact-sql-query.md)。
- SQL 服务帐户现在能够以编程方式标识“启用锁定内存页”和“即时文件初始化”权限。
- 对 TempDB 文件计数、文件大小和文件增长设置的支持。
- 扩展了 showplan XML 中的诊断。
- 轻型按运算符查询执行分析。
- 新的动态管理函数**sys.dm_exec_query_statistics_xml**。
- 用于增量统计的新动态管理函数。
- 已从错误日志中删除了与内存中相关的干扰日志记录消息。
- 改进了 AlwaysOn 延迟诊断。
- 清除了手动更改跟踪。
- **DROP TABLE**支持的复制。
- **大容量插入**到与堆**自动 TABLOCK**下 TF 715。
- 并行**插入...选择**本地临时表的更改。

了解有关在这些修补程序[Service Pack 1 版本说明](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)。

许多数据库引擎改进功能同时适用于 Windows 和 Linux。 当前不支持在 Linux 的数据库引擎功能应该是唯一的例外。 有关详细信息，请参阅[What's New in SQL Server 2017 （数据库引擎）](https://msdn.microsoft.com/library/mt775028)。

## <a name="see-also"></a>另请参阅

有关安装要求、 不受支持的功能区域和已知的问题，请参阅[发行说明有关在 Linux 上的 SQL Server 2017](sql-server-linux-release-notes.md)。

