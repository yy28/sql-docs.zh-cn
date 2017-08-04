---
title: "有关在 Linux 上的 SQL Server 2017 发行说明 |Microsoft 文档"
description: "本主题包含的发行说明，并支持在 Linux 上运行的 SQL Server 2017 的功能。 发行说明也包括针对 RC2 及以前的版本。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: b2f5d26757bd436cfd21076b2a4899376ee60c9f
ms.openlocfilehash: 1907ef1ae99146fe7cdf2ca124af22aabdc29b35
ms.contentlocale: zh-cn
ms.lasthandoff: 08/04/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 版 SQL Server 2017 的发行说明

以下发行说明适用于 Linux 上运行的 SQL Server 2017。 此版本支持适用于 Linux 的多种 SQL Server 数据库引擎功能。 下面的主题分为对于每个版本，以最新版本，RC2 开头的部分。 请参阅每个部分中的信息，了解支持的平台、工具、功能和已知问题。

下表列出了本主题中涵盖的多个 SQL Server 2017 版本。

| 发行版本 | 版本 | 发布日期 |
|-----|-----|-----|
| [RC2](#RC2) | 14.0.900.75 | 8-2017 |
| [RC1](#RC1) | 14.0.800.90 | 7-2017 |
| [CTP 2.1](#ctp21) | 14.0.600.250 | 2017-5 |
| [CTP 2.0](#ctp20) | 14.0.500.272 | 2017-4 |
| [CTP 1.4](#ctp14) | 14.0.405.198 | 2017-3 |
| [CTP 1.3](#ctp13) | 14.0.304.138 | 2017-2 |
| [CTP 1.2](#ctp12) | 14.0.200.24 | 2017-1 |
| [CTP 1.1](#ctp11) | 14.0.100.187 | 2016-12 |
| [CTP 1.0](#ctp10) | 14.0.1.246 | 2016-11 |

## <a id="RC2"></a>RC2 (自 2017 年 8 月)

对于此版本的 SQL Server 引擎版本是 14.0.900.75。

### <a name="supported-platforms"></a>支持的平台

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE]
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> SQL Server 引擎已在此时间测试 1.5 TB 的内存。

### <a name="package-details"></a>包详细信息

下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 请注意，如果使用以下安装指南中的步骤，则无需直接下载这些包：

- [安装 SQL Server 包](sql-server-linux-setup.md)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server 代理包](sql-server-linux-setup-sql-agent.md)

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.900.75-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.900.75-1 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.900.75-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.900.75-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.900.75-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.900.75-1_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.900.75-1_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools for Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新 |

### <a name="unsupported-features-and-services"></a>不支持的功能和服务

Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 事务复制 |
| &nbsp; | 合并复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | 与第三方连接的分布式的查询 |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| &nbsp; | 缓冲池扩展 |
| **SQL Server 代理** |  子系统： CmdExec、 PowerShell、 队列读取器、 SSIS、 SSAS、 SSRS |
| &nbsp; | 警报 |
| &nbsp; | 日志读取器代理 |
| &nbsp; | 变更数据捕获 |
| &nbsp; | 托管备份 |
| **高可用性** | 数据库镜像  |
| **安全性** | 可扩展的密钥管理 |
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题

下列各节描述了在 Linux 上此版本的 SQL Server 自 2017 年 1 RC2 的已知的问题。

#### <a name="general"></a>常规

- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- 默认语言**sa**登录名是英语。

    - **解析**： 更改的语言**sa**具有登录名**ALTER LOGIN**语句。

#### <a name="databases"></a>“数据库”

- 不能使用 mssql conf 实用工具移动 master 数据库。 可以使用 mssql 联赛移动其他系统数据库

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

- 某些算法 （密码套件） 用于传输层安全性 (TLS) 与在 Linux 上的 SQL Server 工作不正常。 这会导致连接失败后尝试连接到 SQL Server，以及建立高可用性组中的副本之间的连接的问题。

   - **解析**： 修改**mssql.conf**通过执行以下操作来禁用有问题的密码套件，Linux 上的 SQL Server 的配置脚本：

      1. 将以下代码添加到 /var/opt/mssql/mssql.conf。

      ```
      [network]
      tlsciphers=ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

      1. 使用以下命令重新启动 SQL Server。
   
      ```
      sudo systemctl restart mssql-server
      ```

#### <a name="remote-database-files"></a>远程数据库文件

- 在此版本中不支持托管 NFS 服务器上的数据库文件。 这包括使用 NFS 共享的磁盘故障转移群集以及数据库在非群集实例上。 我们正在开发启用即将发布的版本中的 NFS 服务器支持。

#### <a name="localization"></a>本地化

- 如果你的区域设置不是在安装过程英语 (en_us)，则必须使用 utf-8 编码在 bash 会话/终端。 如果你使用 ASCII 编码，可能会看到如下错误：

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果你不能使用 utf-8 编码，运行安装程序使用 MSSQL_LCID 环境变量来指定语言选择。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name="full-text-search"></a>全文搜索
- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
你可以在 Linux 上运行 SSIS 包。 有关详细信息，请参阅以下文章：
-   [博客文章宣布推出适用于 Linux 的 SSIS 支持](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)

请注意此版本中的以下已知的问题。

- **Mssql 服务器是**上 Ubuntu 和 Red Hat Enterprise Linux (RHEL) 在此版本中支持包。

- 借助上 Linux CTP 2.1 刷新及更高版本的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 此功能已测试 SQL Server 和 MySQL ODBC 驱动程序，但还需要使用任何 Unicode ODBC 驱动程序观察到 ODBC 规范。 在设计时，你可以提供一个 DSN 或连接字符串以连接到 ODBC 数据中;你还可以使用 Windows 身份验证。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

- 在 Linux 上运行 SSIS 包时，在此版本中不支持以下功能：
  - SSIS 目录数据库
  - SQL 代理计划的包执行
  - Windows 身份验证
  - 第三方组件
  - 变更数据捕获 (CDC)
  - SSIS 横向扩展
  - Azure Feature Pack for SSIS
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 若要保留的日志文件数不能修改。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="RC1"></a>RC1 (自 2017 年 7 月)
对于此版本的 SQL Server 引擎版本是 14.0.800.90。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE]
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 1 TB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 请注意，如果使用以下安装指南中的步骤，则无需直接下载这些包：

- [安装 SQL Server 包](sql-server-linux-setup.md)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server 代理包](sql-server-linux-setup-sql-agent.md)

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.800.90-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| SLES RPM 包 | 14.0.800.90-2 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.800.90-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.800.90-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.800.90-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.800.90-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.800.90-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.800.90-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.800.90-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.800.90-2_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.800.90-2_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools for Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新 |

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 事务复制 |
| &nbsp; | 合并复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **SQL Server 代理** |  子系统： CmdExec、 PowerShell、 队列读取器、 SSIS、 SSAS、 SSRS |
| &nbsp; | 警报 |
| &nbsp; | 日志读取器代理 |
| &nbsp; | 变更数据捕获 |
| &nbsp; | 托管备份 |
| **高可用性** | 数据库镜像  |
| &nbsp; | 可用性组的滚动升级 |
| **安全性** | 可扩展的密钥管理 |
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
下列各节描述了在 Linux 上此版本的 SQL Server 自 2017 年 1 RC1 的已知的问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- 默认语言**sa**登录名是英语。

    - **解析**： 更改的语言**sa**具有登录名**ALTER LOGIN**语句。

#### <a name="databases"></a>“数据库”

- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

#### <a name="remote-database-files"></a>远程数据库文件

- 在此版本中不支持托管 NFS 服务器上的数据库文件。 这包括使用 NFS 共享的磁盘故障转移群集以及数据库在非群集实例上。 我们正在开发启用即将发布的版本中的 NFS 服务器支持。

#### <a name="cross-platform-availability-groups-and-distributed-availability-groups"></a>跨平台可用性组和分布式的可用性组

- 由于已知问题，使用在 Windows 和 Linux 上承载的实例上的副本创建可用性组的工作不在此版本中。 这包括分布式的可用性组。 此修补程序将在即将发布的版本候选版本中可用。 

#### <a name="server-collation"></a>服务器排序规则

- 当使用 MSSQL_COLLATION 重写，或如果执行操作的本地化 （非英语） 安装，则可能在尝试设置生成转储服务器排序规则时，SQL Server 将命中死锁。 安装程序不会成功完成，但是服务器排序规则将是尚未设置。 解决方法是只需运行。 / mssql conf 排序规则集，然后输入所需的出现提示时的排序规则名称 (在行上的错误日志中找不到排序规则名称:"尝试更改到的默认排序规则...")。 
 
#### <a name="localization"></a>本地化

- 如果你的区域设置不是在安装过程英语 (en_us)，则必须使用 utf-8 编码在 bash 会话/终端。 如果你使用 ASCII 编码，可能会看到如下错误：

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果你不能使用 utf-8 编码，运行安装程序使用 MSSQL_LCID 环境变量来指定语言选择。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

#### <a name = "fci"></a>共享磁盘群集实例升级

RC1 中群集资源代理设置的虚拟服务器名称，像在 Windows 上的故障转移群集实例。 RC1 之前`@@servername`上的共享磁盘群集返回特定节点名称，在故障转移后`@@servername`返回不同的值。 在 RC1 共享的磁盘群集实例的 serverName 资源添加到群集时使用的资源名称更新。 因此，群集将需要重新启动 SQL Server 后手动故障转移期间升级-如下所示的以下步骤：

1. 首先升级辅助 （被动） 的群集节点。
   - 升级**mssql server**包。
   - 升级**mssql-服务器-ha**包。
1. 手动故障转移到已升级的节点。
   `pcs resource move <resourceName>`
   - 资源最初失败，因为资源代理检查实际和预期 serverName。 预期的服务器名称将会不同。
   - 群集将重新启动 SQL Server 的同一节点上的资源。 这将更新服务器名称。
1. 升级其他节点。 
   - 升级**mssql server**包。
   - 升级**mssql-服务器-ha**包。
1. 删除通过手动资源移动添加该约束。 请参阅[手动故障转移群集](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md#failManual)。
2. 如果需要，故障回复到原始主节点。 

#### <a name="availability-group"></a>可用性组

在 Linux 上，滚动升级的 SQL Server 自 2017 年 1 CTP 2.1 到 RC1 不支持。 升级辅助副本之后，它将断开连接从主副本中，直至升级主要副本。 Microsoft 规划以解决此问题在未来版本。

#### <a name="full-text-search"></a>全文搜索
- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

#### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- **Mssql 服务器是**包在此版本中不支持在 SUSE 上。 当前支持在 Ubuntu 上和 Red Hat Enterprise Linux (RHEL) 上。

- 在 Linux 上运行 SSIS 包时，在此版本中不支持以下功能：
  - SSIS 目录数据库
  - SQL 代理计划的包执行
  - Windows 身份验证
  - 第三方组件
  - 变更数据捕获 (CDC)
  - SSIS 横向扩展
  - Azure Feature Pack for SSIS
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

有关在 Linux 上的 SSIS 的详细信息，请参阅以下文章：
-   [在 Linux 上安装 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [提取、 转换和加载使用 SSIS 的 Linux 上的数据](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 若要保留的日志文件数不能修改。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp21"></a>CTP 2.1 (2017 年 5 月)
此次发布的 SQL Server 引擎版本是 14.0.600.250。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE]
> 你需要至少 3.25 GB 的内存来运行在 Linux 上的 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 1 TB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 不需要直接下载这些包，如果你在以下安装指南中使用的步骤：

- [安装 SQL Server 包](sql-server-linux-setup.md)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server 代理包](sql-server-linux-setup-sql-agent.md)

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.600.250-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| SLES RPM 包 | 14.0.600.250-2 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.600.250-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.600.250-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.600.250-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.600.250-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.600.250-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.600.250-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.600.250-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.600.250-2_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.600.250-2_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools for Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新 (1.12) |

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **高可用性** | 数据库镜像  |
| **安全性** | Active Directory 身份验证 |
| &nbsp; | Windows 身份验证 |
| &nbsp; | 可扩展的密钥管理 |
| &nbsp; | 对 SSL 或 TLS 使用用户提供的证书 |
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
下列各节描述了在 Linux 上此版本的 SQL Server 自 2017 年 1 CTP 2.1 的已知的问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- 默认语言**sa**登录名是英语。

    - **解析**： 更改的语言**sa**具有登录名**ALTER LOGIN**语句。

#### <a name="databases"></a>“数据库”
- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

#### <a name="always-on-availability-group"></a>Always On 可用性组
- `sys.fn_hadr_backup_is_preffered_replica`并不适用于`CLUSTER_TYPE=NONE`或`CLUSTER_TYPE=EXTERNAL`因为它依赖于 WSFC 复制群集注册表项的不可用。 我们正在研究，希望通过其他功能来提供类似功能。 

#### <a name="full-text-search"></a>全文搜索
- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

#### <a name="sql-agent"></a>SQL 代理
- 以下组件和子系统 SQL 代理作业的当前不支持在 Linux 上：

    - 子系统：CmdExec、PowerShell、复制分发服务器、Snapshot、Merge、队列读取器、SSIS、SSAS、SSRS
    - 警报
    - DB 邮件
    - 日志读取器代理 
    - 变更数据捕获

#### <a name="sqlpackage"></a>SqlPackage
- 使用 SqlPackage 要求指定文件的绝对路径。 使用相对路径将映射"/ tmp/sqlpackage 下文件。\<代码 \> /系统/system32"文件夹。 

  - **解析**： 使用绝对文件路径。

- SqlPackage 显示具有的文件的位置"c:\\"前缀。

#### <a name="ssis"></a> SQL Server Integration Services (SSIS)
你可以在 Linux 上运行 SSIS 包。 有关详细信息，请参阅[博客文章宣布推出适用于 Linux 的 SSIS 支持](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。 请注意此版本中的以下已知的问题。

- **Mssql 服务器是**此时中，将包仅支持在 Ubuntu 上。

- 在 Linux 上运行 SSIS 包时，不支持以下功能：
  - SSIS 目录数据库
  - SQL 代理计划包执行
  - Windows 身份验证
  - 第三方组件
  - 第三方 ODBC 驱动程序
  - ODBC 连接管理器、 源和目标 （在 Linux CTP 2.1 刷新的 SSIS 支持）
  - 变更数据捕获 (CDC)
  - 扩展
  - Azure 功能包
  - Hadoop 和 HDFS 支持
  - Microsoft Connector for SAP BW

借助 Linux CTP 2.1 刷新的 SSIS，SSIS 包可以在 Linux 上使用 ODBC 连接。 有关详细信息，请参阅[博客文章在 Linux 上的宣布推出的 ODBC 支持](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 若要保留的日志文件数不能修改。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp20"></a>CTP 2.0 (自 2017 年 4 月)
此次发布的 SQL Server 引擎版本是 14.0.500.272。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 和 16.10 | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 1 TB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 请注意，如果使用以下安装指南中的步骤，则无需直接下载这些包：

- [安装 SQL Server 包](sql-server-linux-setup.md)
- [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
- [安装 SQL Server 代理包](sql-server-linux-setup-sql-agent.md)

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.500.272-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| SLES RPM 包 | 14.0.500.272-2 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.500.272-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.500.272-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.500.272-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.500.272-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.500.272-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |
| Ubuntu 16.10 Debian 包 | 14.0.500.272-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.500.272-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.500.272-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.500.272-2_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.500.272-2_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的候选发布版 2 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools for Visual Studio-候选发布版 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新版本 (0.2.1) |

> [!NOTE] 
> 上文中指定的 SQL Server Management Studio 和 SQL Server Data Tools 版本是候选版本，因此不建议在生产中使用。

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **高可用性** | 数据库镜像  |
| **安全性** | Active Directory 身份验证 |
| &nbsp; | Windows 身份验证 |
| &nbsp; | 可扩展的密钥管理 |
| &nbsp; | 对 SSL 或 TLS 使用用户提供的证书 |
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
以下部分介绍 Linux 上此次发布的 SQL Server 2017 CTP 2.0 的已知问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- 默认语言**sa**登录名是英语。

    - **解析**： 更改的语言**sa**具有登录名**ALTER LOGIN**语句。

#### <a name="databases"></a>“数据库”
- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

#### <a name="always-on-availability-group"></a>Always On 可用性组
- 所有 HA 配置-这意味着作为资源添加到 Pacemaker 群集-使用前 CTP2.0 包创建可用性组不是使用新的包向后兼容的。 删除所有以前配置的群集的资源，然后创建新的可用性组用于`CLUSTER_TYPE=EXTERNAL`。 请参阅[配置 Always On 可用性组在 Linux 上的 SQL Server 的](sql-server-linux-availability-group-configure-ha.md)。
- 使用创建的可用性组`CLUSTER_TYPE=NONE`和未添加为群集中的资源将升级后继续工作。 用于读取缩放方案。 请参阅[在 Linux 上的 SQL Server 的配置读取缩放可用性组](sql-server-linux-availability-group-configure-rs.md)。
- `sys.fn_hadr_backup_is_preffered_replica`并不适用于`CLUSTER_TYPE=NONE`或`CLUSTER_TYPE=EXTERNAL`因为它依赖于 WSFC 复制群集注册表项的不可用。 我们正在研究，希望通过其他功能来提供类似功能。 

#### <a name="full-text-search"></a>全文搜索
- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

- 朝鲜语的断字符需要几秒钟才能加载，将生成第一次使用错误。 在此初始错误之后，它应会正常工作。

#### <a name="sql-agent"></a>SQL 代理
- 以下组件和子系统 SQL 代理作业的当前不支持在 Linux 上：

    - 子系统：CmdExec、PowerShell、复制分发服务器、Snapshot、Merge、队列读取器、SSIS、SSAS、SSRS
    - 警报
    - DB 邮件
    - 日志读取器代理 
    - 变更数据捕获

#### <a name="sqlpackage"></a>SqlPackage
- 使用 SqlPackage 要求指定文件的绝对路径。 使用相对路径将映射"/ tmp/sqlpackage 下文件。\<代码 \> /系统/system32"文件夹。 

    - **解析**： 使用绝对文件路径。

- SqlPackage 显示具有的文件的位置"c:\\"前缀。

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 若要保留的日志文件数不能修改。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp14"></a>CTP 1.4 (自 2017 年 3 月)
此次发布的 SQL Server 引擎版本是 14.0.405.198。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 和 16.10 | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 1 TB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 请注意，如果使用下面的安装指南中的步骤，则无需直接下载这些包
-   [安装 SQL Server 包](sql-server-linux-setup.md)
-   [安装全文搜索包](sql-server-linux-setup-full-text-search.md)
-   [安装 SQL Server 代理包](sql-server-linux-setup-sql-agent.md)

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.405.200-1 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.405.200-1 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.405.200-1.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.405.200-1.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.405.200-1.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.405.200-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.405.200-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |
| Ubuntu 16.10 Debian 包 | 14.0.405.200-1 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.405.200-1_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.405.200-1_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.405.200-1_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.405.200-1_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的候选发布版 2 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools for Visual Studio-候选发布版 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新版本 (0.2.1) |

> [!NOTE] 
> 上文中指定的 SQL Server Management Studio 和 SQL Server Data Tools 版本是候选版本，因此不建议在生产中使用。

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **高可用性** | 数据库镜像  |
| **安全性** | Active Directory 身份验证 |
| &nbsp; | Windows 身份验证 |
| &nbsp; | 可扩展的密钥管理 |
| &nbsp; | 对 SSL 或 TLS 使用用户提供的证书 |
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
以下部分介绍 Linux 上此次发布的 SQL Server 2017 CTP 1.4 的已知问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 不运行该命令`ALTER SERVICE MASTER KEY REGENERATE`。 没有将导致 SQL Server 以变得不稳定的一个已知的 bug。 如果需要重新生成服务主密钥，应备份数据库文件，卸载并重新安装 SQL Server，然后再次还原数据库文件。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 在 Linux 中的某些时区名称不完全映射到 Windows 时区名称。

    - **解析**： 使用从 TZID 列中的时区名称映射为： 上的 Windows 的部分表[Unicode.org 文档页](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)。

- SQL Server 引擎需要终止与 CR LF （Windows 样式行格式设置） 的文本文件中的行。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- 所有日志文件，并以 utf-16 进行编码，错误日志。

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- **CREATE ASSEMBLY**时尝试使用文件将无法工作。 使用**FROM \<bits\>** 方法改为现在。 

#### <a name="databases"></a>“数据库”
- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

#### <a name="always-on-availability-group"></a>Always On 可用性组
- Always On 可用性组之后升级 HA 包 (mssql-服务器-ha)，在 Linux 上使用 CTP 1.3 创建的群集的资源将失败。 

   - **解析**： 升级 HA 包之前，请将群集资源参数设置`notify=true`。 
   
      - 下面的示例在一个名为资源上设置了群集资源参数**ag1** RHEL 或 Ubuntu 上： 

      ```bash
      sudo pcs resource update ag1-master notify=true
      ```

      - 对于 SLES，更新可用性组资源配置，以添加`notify=true`。  

      ```bash
      crm configure edit ms-ag_cluster 
      ```

      添加`notify=true`并保存资源配置。

- 如果副本处于同步提交模式下，alwayson 可用性组在 Linux 中可能会遭受数据丢失。 请参阅适用于 Linux 分发版的详细信息。 

   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

#### <a name="full-text-search"></a>全文搜索
- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

- 朝鲜语的断字符需要几秒钟才能加载，将生成第一次使用错误。 在此初始错误之后，它应会正常工作。

#### <a name="sql-agent"></a>SQL 代理
- 以下组件和子系统 SQL 代理作业的当前不支持在 Linux 上：
    - 子系统：CmdExec、PowerShell、复制分发服务器、Snapshot、Merge、队列读取器、SSIS、SSAS、SSRS
    - 警报
    - DB 邮件
    - 日志传送
    - 日志读取器代理 
    - 变更数据捕获

#### <a name="in-memory-oltp"></a>内存中 OLTP
- 仅在 /var/opt/mssql 目录中创建内存中 OLTP 数据库。 有关详细信息，请访问[内存中 OLTP 主题](sql-server-linux-performance-get-started.md#use-in-memory-oltp)。  

#### <a name="sqlpackage"></a>SqlPackage
- 使用 SqlPackage 要求指定文件的绝对路径。 使用相对路径将映射"/ tmp/sqlpackage 下文件。\<代码 \> /系统/system32"文件夹。 

    - **解析**： 使用绝对文件路径。

- SqlPackage 显示具有的文件的位置"c:\\"前缀。

    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 文件浏览器仅限于"c:\\"作用域，哪些解析为/var/选择/mssql/Linux 上。 若要使用其他路径，生成的 UI 操作的脚本，并将 c:\\路径替换为 Linux 路径。 然后在 SSMS 中手动执行脚本。

- 若要保留的日志文件数不能修改。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a id="ctp13"></a>CTP 1.3 (自 2017 年 2 月)
此次发布的 SQL Server 引擎版本是 14.0.304.138。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 和 16.10 | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 1 TB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 如果使用中的步骤，请注意，不需要下载这些直接包[安装指南](sql-server-linux-setup.md)。

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| Red Hat RPM 包 | 14.0.304.138-1 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[mssql-服务器-ha 高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[mssql server fts 的全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.304.138-1 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-14.0.304.138-1.x86_64.rpm)</br>[mssql-服务器-ha 高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-ha-14.0.304.138-1.x86_64.rpm)</br>[mssql server fts 的全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server/mssql-server-fts-14.0.304.138-1.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.304.138-1 | [mssql server 引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[mssql-服务器-ha 高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[mssql server fts 的全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |
| Ubuntu 16.10 Debian 包 | 14.0.304.138-1 | [mssql server 引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.304.138-1_amd64.deb)</br>[mssql-服务器-ha 高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.304.138-1_amd64.deb)</br>[mssql server fts 的全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.10/mssql-server/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.304.138-1_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的候选发布版 2 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=840957) | 17.0 |
| [SQL Server Data Tools for Visual Studio-候选发布版 2](https://go.microsoft.com/fwlink/?linkid=837939) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新版本 (0.2.1) |

> [!NOTE] 
> 上文中指定的 SQL Server Management Studio 和 SQL Server Data Tools 版本是候选版本，因此不建议在生产中使用。

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **高可用性** | 数据库镜像  |
| **安全性** | Active Directory 身份验证 |
| &nbsp; | Windows 身份验证 |
| &nbsp; | 可扩展的密钥管理 |
| &nbsp; | 对 SSL 或 TLS 使用用户提供的证书 |
| **服务** | SQL Server 代理 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
以下部分介绍 Linux 上此次发布的 SQL Server 2017 CTP 1.3 的已知问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 不运行该命令`ALTER SERVICE MASTER KEY REGENERATE`。 没有将导致 SQL Server 以变得不稳定的一个已知的 bug。 如果需要重新生成服务主密钥，应备份数据库文件，卸载并重新安装 SQL Server，然后再次还原数据库文件。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 在 Linux 中的某些时区名称不完全映射到 Windows 时区名称。

    - **解析**： 使用从 TZID 列中的时区名称映射为： 上的 Windows 的部分表[Unicode.org 文档页](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)。

- SQL Server 引擎需要终止与 CR LF （Windows 样式行格式设置） 的文本文件中的行。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- 所有日志文件，并以 utf-16 进行编码，错误日志。

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- **CREATE ASSEMBLY**时尝试使用文件将无法工作。 使用**FROM \<bits\>** 方法改为现在。 

#### <a name="databases"></a>“数据库”
- 不支持更改 TempDB 数据和日志文件的位置。

- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

- 如果副本处于同步提交模式下，alwayson 可用性组在 Linux 中可能会遭受数据丢失。 请参阅 
 
   - [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   - [SLES](sql-server-linux-availability-group-cluster-sles.md)
   - [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   
#### <a name="full-text-search"></a>全文搜索
- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

- 朝鲜语的断字符需要几秒钟才能加载，将生成第一次使用错误。 在此初始错误之后，它应会正常工作。

#### <a name="in-memory-oltp"></a>内存中 OLTP
- 仅在 /var/opt/mssql 目录中创建内存中 OLTP 数据库。 有关详细信息，请访问[内存中 OLTP 主题](sql-server-linux-performance-get-started.md#use-in-memory-oltp)。  

#### <a name="sqlpackage"></a>SqlPackage
- 使用 SqlPackage 要求指定文件的绝对路径。 使用相对路径将映射“/tmp/sqlpackage./<code/>/system/system32”文件夹下的文件。 

    - **解析**： 使用绝对文件路径。

- SqlPackage 显示具有的文件的位置"c:\\"前缀。

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 和 ODBC 
- SQL Server 命令行工具 （mssql 工具） 和 ODBC 驱动程序 (msodbcsql) 依赖于自定义 unixODBC 驱动程序管理器。 如果之前已安装了 unixODBC 驱动程序管理器，则会导致冲突。 

    - **解析**: Ubuntu 上将自动解决冲突。 当系统提示要卸载现有的 unixODBC 驱动程序管理器，请键入 y，并继续安装。 在 RedHat，你将必须手动删除现有 unixODBC 驱动程序管理器使用`yum remove unixODBC`。 我们正在修复此限制的 RHEL 和 SUSE，并且应具有更新为你很快。  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 尚不支持 SQL Server 代理。 因此，SSMS 中的 SQL Server 代理功能目前在 Linux 上无效。

- 文件浏览器仅限于"c:\\"作用域，哪些解析为/var/选择/mssql/Linux 上。 若要使用其他路径，生成的 UI 操作的脚本，并将 c:\\路径替换为 Linux 路径。 然后在 SSMS 中手动执行脚本。

- 若要保留的日志文件数不能修改。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp12-ctp-12-january-2017"></a><a id="ctp12">CTP 1.2 (2017 年 1 月)
此次发布的 SQL Server 引擎版本是 14.0.200.24。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [安装指南](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS 和 16.10 | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 256GB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 如果使用中的步骤，请注意，不需要下载这些直接包[安装指南](sql-server-linux-setup.md)。

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| RPM 包 | 14.0.200.24-2 | [mssql server 14.0.200.24-2 引擎 RPM 程序包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.200.24-2.x86_64.rpm)</br>[mssql server 14.0.200.24-2 高可用性 RPM 程序包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.200.24-2.x86_64.rpm) | 
| Debian 包 | 14.0.200.24-2 | [mssql server 14.0.200.24-2 引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.200.24-2_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的候选发布版 1 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools for Visual Studio-候选发布版 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新版本 (0.2) |

> [!NOTE] 
> 上文中指定的 SQL Server Management Studio 和 SQL Server Data Tools 版本是候选版本，因此不建议在生产中使用。

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 全文搜索 |
| &nbsp; | 复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **高可用性** | Always On 可用性组 |
| &nbsp; | 数据库镜像  |
| **安全性** | Active Directory 身份验证 |
| &nbsp; | Windows 身份验证 |
| &nbsp; | 可扩展的密钥管理 |
| &nbsp; | 对 SSL 或 TLS 使用用户提供的证书 |
| **服务** | SQL Server 代理 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
以下部分介绍 Linux 上此次发布的 SQL Server 2017 CTP 1.2 的已知问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 不运行该命令`ALTER SERVICE MASTER KEY REGENERATE`。 没有将导致 SQL Server 以变得不稳定的一个已知的 bug。 如果需要重新生成服务主密钥，应备份数据库文件，卸载并重新安装 SQL Server，然后再次还原数据库文件。

- 从 ocf:sql:fci 更改为 ocf:mssql:fci SQL 资源的资源名称。 有关配置共享的磁盘故障转移群集可以找到更多详细信息[此处](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure)。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 在 Linux 中的某些时区名称不完全映射到 Windows 时区名称。

    - **解析**： 使用从 TZID 列中的时区名称映射为： 上的 Windows 的部分表[Unicode.org 文档页](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)。

- SQL Server 引擎需要终止与 CR LF （Windows 样式行格式设置） 的文本文件中的行。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- 所有日志文件，并以 utf-16 进行编码，错误日志。

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- **CREATE ASSEMBLY**时尝试使用文件将无法工作。 使用**FROM \<bits\>** 方法改为现在。 

#### <a name="databases"></a>“数据库”
- 不支持更改 TempDB 数据和日志文件的位置。

- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

#### <a name="in-memory-oltp"></a>内存中 OLTP
- 仅在 /var/opt/mssql 目录中创建内存中 OLTP 数据库。 这些数据库还需要具有"c:\\"表示法被引用时。 有关详细信息，请访问[内存中 OLTP 主题](sql-server-linux-performance-get-started.md#use-in-memory-oltp)。  

#### <a name="sqlpackage"></a>SqlPackage
- 使用 SqlPackage 要求指定文件的绝对路径。 使用相对路径将映射"/ tmp/sqlpackage 下文件。\<代码 \> /系统/system32"文件夹。 

    - **解析**： 使用绝对文件路径。

- SqlPackage 显示具有的文件的位置"c:\\"前缀。

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 和 ODBC 
- 如果你有较旧版本的 SQL Server 命令行工具 （mssql 工具） 和 ODBC 驱动程序 (msodbcsql)，你可能已安装自定义 unixODBC 驱动程序管理器 (unixODBC utf16)。 由于我们不再使用的自定义驱动程序管理器，这可能会导致潜在的冲突。 

    - **解析**： 在 Ubuntu 和 SLES 上，将自动解决冲突。 当系统提示要卸载现有的 unixODBC 驱动程序管理器，请键入 y，并继续安装。 在 RedHat，你将必须手动删除现有 unixODBC 驱动程序管理器使用`yum remove unixODBC-utf16 unixODBC-utf16-devel`，然后重试安装。
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 尚不支持 SQL Server 代理。 因此，SSMS 中的 SQL Server 代理功能目前在 Linux 上无效。

- 文件浏览器仅限于"c:\\"作用域，哪些解析为/var/选择/mssql/Linux 上。 若要使用其他路径，生成的 UI 操作的脚本，并将 c:\\路径替换为 Linux 路径。 然后在 SSMS 中手动执行脚本。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp11-ctp-11-december-2016"></a><a id="ctp11">CTP 1.1 (2016 年 12 月)
此次发布的 SQL Server 引擎版本是 14.0.100.187。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 工作站、服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS 和 16.10 | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 256GB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 如果使用中的步骤，请注意，不需要下载这些直接包[安装指南](sql-server-linux-setup.md)。

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| RPM 包 | 14.0.100.187-1 | [mssql server 14.0.100.187-1 引擎 RPM 程序包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.100.187-1.x86_64.rpm)</br>[mssql server 14.0.100.187-1 高可用性 RPM 程序包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.100.187-1.x86_64.rpm) | 
| Debian 包 | 14.0.100.187-1 | [mssql server 14.0.100.187-1 引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.100.187-1_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的候选发布版 1 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools for Visual Studio-候选发布版 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新版本 (0.2) |

> [!NOTE] 
> 上文中指定的 SQL Server Management Studio 和 SQL Server Data Tools 版本是候选版本，因此不建议在生产中使用。

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 全文搜索 |
| &nbsp; | 复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **高可用性** | Always On 可用性组 |
| &nbsp; | 数据库镜像  |
| **安全性** | Active Directory 身份验证 |
| &nbsp; | Windows 身份验证 |
| &nbsp; | 可扩展的密钥管理 |
| &nbsp; | 对 SSL 或 TLS 使用用户提供的证书 |
| **服务** | SQL Server 代理 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
以下部分介绍 Linux 上此次发布的 SQL Server 2017 CTP 1.1 的已知问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 不运行该命令`ALTER SERVICE MASTER KEY REGENERATE`。 没有将导致 SQL Server 以变得不稳定的一个已知的 bug。 如果需要重新生成服务主密钥，应备份数据库文件，卸载并重新安装 SQL Server，然后再次还原数据库文件。

- 从 ocf:sql:fci 更改为 ocf:mssql:fci SQL 资源的资源名称。 有关配置共享的磁盘故障转移群集可以找到更多详细信息[此处](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-shared-disk-cluster-red-hat-7-configure)。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 在 Linux 中的某些时区名称不完全映射到 Windows 时区名称。

    - **解析**： 使用从 TZID 列中的时区名称映射为： 上的 Windows 的部分表[Unicode.org 文档页](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)。

- SQL Server 引擎需要终止与 CR LF （Windows 样式行格式设置） 的文本文件中的行。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- 所有日志文件，并以 utf-16 进行编码，错误日志。

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- **CREATE ASSEMBLY**时尝试使用文件将无法工作。 使用**FROM \<bits\>** 方法改为现在。 

#### <a name="databases"></a>“数据库”
- 不支持更改 TempDB 数据和日志文件的位置。

- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

#### <a name="in-memory-oltp"></a>内存中 OLTP
- 仅在 /var/opt/mssql 目录中创建内存中 OLTP 数据库。 这些数据库还需要具有"c:\"表示法被引用时。 有关详细信息，请访问[内存中 OLTP 主题](sql-server-linux-performance-get-started.md#use-in-memory-oltp)。  

#### <a name="sqlpackage"></a>SqlPackage
- 使用 SqlPackage 要求指定文件的绝对路径。 使用相对路径将映射"/ tmp/sqlpackage 下文件。\<代码 \> /系统/system32"文件夹。 

    - **解析**： 使用绝对文件路径。

- SqlPackage 显示具有的文件的位置"c:\\"前缀。

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 和 ODBC 
- SQL Server 命令行工具 （mssql 工具） 和 ODBC 驱动程序 (msodbcsql) 依赖于自定义 unixODBC 驱动程序管理器。 如果之前已安装了 unixODBC 驱动程序管理器，则会导致冲突。 

    - **解析**: Ubuntu 上将自动解决冲突。 当系统提示要卸载现有的 unixODBC 驱动程序管理器，请键入 y，并继续安装。 在 RedHat，你将必须手动删除现有 unixODBC 驱动程序管理器使用`yum remove unixODBC`。 我们正在修复此限制的 RHEL 和 SUSE，并且应具有更新为你很快。  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 尚不支持 SQL Server 代理。 因此，SSMS 中的 SQL Server 代理功能目前在 Linux 上无效。

- 文件浏览器仅限于"c:\\"作用域，哪些解析为/var/选择/mssql/Linux 上。 若要使用其他路径，生成的 UI 操作的脚本，并将 c:\\路径替换为 Linux 路径。 然后在 SSMS 中手动执行脚本。

v

![分离栏图形](./media/sql-server-linux-release-notes/seperationbar3.png)

## <a name="a-idctp10-ctp-10-november-2016"></a><a id="ctp10">CTP 1.0 (2016 年 11 月)
此次发布的 SQL Server 引擎版本是 14.0.1.246。

### <a name="supported-platforms"></a>支持的平台 

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.2 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
| Ubuntu 16.04LTS | EXT4 | [安装指南](quickstart-install-connect-ubuntu.md) | 
| Windows、Mac 或 Linux 上的 Docker 引擎 1.8 及更高版本 | N/A | [安装指南](quickstart-install-connect-docker.md) | 

> [!NOTE] 
> 至少需要 3.25GB 内存才能在 Linux 上运行 SQL Server。
> 目前，已测试出 SQL Server 引擎最多可占用 256GB 内存。

### <a name="package-details"></a>包详细信息
下表列出了包的详细信息以及 RPM 和 Debian 包的下载位置。 如果使用中的步骤，请注意，不需要下载这些直接包[安装指南](sql-server-linux-setup.md)。

| “包” | 包版本 | 下载 |
|-----|-----|-----|
| RPM 包 | 14.0.1.246-6 | [mssql server 14.0.1.246-6 引擎 RPM 程序包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.1.246-6.x86_64.rpm)</br>[mssql server 14.0.1.246-6 高可用性 RPM 程序包](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.1.246-6.x86_64.rpm) | 
| Debian 包 | 14.0.1.246-6 | [mssql server 14.0.1.246-6 引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server/pool/main/m/mssql-server/mssql-server_14.0.1.246-6_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的候选发布版 1 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?LinkID=835608) | 17.0 |
| [SQL Server Data Tools for Visual Studio-候选发布版 1](https://go.microsoft.com/fwlink/?LinkID=835150) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新版本 (0.1.5) |

> [!NOTE] 
> 上文中指定的 SQL Server Management Studio 和 SQL Server Data Tools 版本是候选版本，因此不建议在生产中使用。

### <a name="unsupported-features-and-services"></a>不支持的功能和服务
Linux 目前不支持以下功能和服务。 预览计划的每月更新中将逐步启用对这些功能的支持。

| 区域 | 不支持的功能或服务 |
|-----|-----|
| **数据库引擎** | 全文搜索 |
| &nbsp; | 复制 |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Distributed Query |
| &nbsp; | 系统扩展的存储过程（XP_CMDSHELL 等） |
| &nbsp; | Filetable |
| &nbsp; | 带有 EXTERNAL_ACCESS 或 UNSAFE 权限集的 CLR 程序集 |
| **高可用性** | Always On 可用性组 |
| &nbsp; | 数据库镜像  |
| **安全性** | Active Directory 身份验证 |
| &nbsp; | Windows 身份验证 |
| &nbsp; | 可扩展的密钥管理 |
| &nbsp; | 对 SSL 或 TLS 使用用户提供的证书 |
| **服务** | SQL Server 代理 |
| &nbsp; | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Integration Services | 
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题
以下部分介绍 Linux 上此次发布的 SQL Server 2017 CTP1 的已知问题。

#### <a name="general"></a>常规
- SQL Server 安装需要 15 个字符或更少的所在的主机名的长度。 

    - **解析**： 将/等/主机名中的名称更改为某个地方 15 个字符长或更少。

- 手动将系统时间设置为时间倒移，会导致 SQL Server 停止更新 SQL Server 中的内部系统时间。

    - **解析**： 重新启动 SQL Server。

- 在 Linux 中的某些时区名称不完全映射到 Windows 时区名称。

    - **解析**： 使用从 TZID 列中的时区名称映射为： 上的 Windows 的部分表[Unicode.org 文档页](http://www.unicode.org/cldr/charts/latest/supplemental/zone_tzid.html)。

- SQL Server 引擎需要终止与 CR LF （Windows 样式行格式设置） 的文本文件中的行。

- 仅支持单个实例安装。

    - **解析**： 如果你想要指定主机上具有多个实例，请考虑使用 Vm 或 Docker 容器。 

- 所有日志文件，并以 utf-16 进行编码，错误日志。

- SQL Server 配置管理器无法连接到 Linux 上的 SQL Server。

- **CREATE ASSEMBLY**时尝试使用文件将无法工作。 使用**FROM \<bits\>** 方法改为现在。

#### <a name="databases"></a>“数据库”
- 不支持更改 TempDB 数据和日志文件的位置。

- 不能使用 mssql conf 实用工具移动系统数据库。

- 还原已在 Windows 上的 SQL 服务器备份数据库时，必须使用**WITH MOVE** Transact SQL 语句中的子句。

- 在 Linux 上运行的 SQL Server 上不支持需要 Microsoft 分布式事务处理协调器服务的分布式事务。 支持从 SQL Server 到 SQL Server 的分布式事务。

#### <a name="in-memory-oltp"></a>内存中 OLTP
- 仅在 /var/opt/mssql 目录中创建内存中 OLTP 数据库。 这些数据库还需要具有"c:\\"表示法被引用时。 有关详细信息，请访问[内存中 OLTP 主题](sql-server-linux-performance-get-started.md#use-in-memory-oltp)。  

#### <a name="sqlpackage"></a>SqlPackage
- 使用 SqlPackage 要求指定文件的绝对路径。 使用相对路径将映射"/ tmp/sqlpackage 下文件。\<代码 \> /系统/system32"文件夹。 

    - **解析**： 使用绝对文件路径。

- SqlPackage 显示具有的文件的位置"c:\\"前缀。

#### <a name="sqlcmdbcp--odbc"></a>Sqlcmd/BCP 和 ODBC 
- SQL Server 命令行工具 （mssql 工具） 和 ODBC 驱动程序 (msodbcsql) 依赖于自定义 unixODBC 驱动程序管理器。 如果之前已安装了 unixODBC 驱动程序管理器，则会导致冲突。 

    - **解析**: Ubuntu 上将自动解决冲突。 当系统提示要卸载现有的 unixODBC 驱动程序管理器，请键入 y，并继续安装。 在 RedHat，你将必须手动删除现有 unixODBC 驱动程序管理器使用`yum remove unixODBC`。 我们正在修复此限制的 RHEL 和 SUSE，并且应具有更新为你很快。  
    
#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
以下限制适用于 Windows 中连接到 Linux 上 SQL Server 的 SSMS。

- 不支持维护计划。

- 不支持管理数据仓库 (MDW) 和 SSMS 中的数据收集器。 

- 具有 Windows 身份验证或 Windows 事件日志选项的 SSMS UI 组件不适用于 Linux。 仍可通过其它选项（如 SQL 登录名）使用这些功能。 

- 尚不支持 SQL Server 代理。 因此，SSMS 中的 SQL Server 代理功能目前在 Linux 上无效。

- 文件浏览器仅限于"c:\\"作用域，哪些解析为/var/选择/mssql/Linux 上。 若要使用其他路径，生成的 UI 操作的脚本，并将 c:\\路径替换为 Linux 路径。 然后在 SSMS 中手动执行脚本。

### <a name="next-steps"></a>后续步骤

若要开始，请参阅以下快速入门教程：

- [在 Red Hat Enterprise Linux 上安装](quickstart-install-connect-red-hat.md)
- [在 SUSE Linux Enterprise Server 上安装](quickstart-install-connect-suse.md)
- [在 Ubuntu 上安装](quickstart-install-connect-ubuntu.md)
- [在 Docker 上运行](quickstart-install-connect-ubuntu.md)
<br/>
<br/>

