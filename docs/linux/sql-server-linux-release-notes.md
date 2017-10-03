---
title: "有关在 Linux 上的 SQL Server 2017 发行说明 |Microsoft 文档"
description: "本主题包含的发行说明，并支持在 Linux 上运行的 SQL Server 2017 的功能。 发行说明也包括针对最新版本和多个以前的版本。"
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.translationtype: MT
ms.sourcegitcommit: 7811cfe9238c92746673fac4fce40a4af44d6dcd
ms.openlocfilehash: 80c0813accf9f84204f057b9ef4efcad69142ec2
ms.contentlocale: zh-cn
ms.lasthandoff: 10/02/2017

---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Linux 版 SQL Server 2017 的发行说明

以下发行说明适用于 Linux 上运行的 SQL Server 2017。 此版本支持适用于 Linux 的多种 SQL Server 数据库引擎功能。 下面的主题分为对于每个版本，以最新的常规开头部分正式版 (GA) 发布版本和以前的两个版本。 请参阅每个部分中的信息，了解支持的平台、工具、功能和已知问题。

下表列出 SQL Server 自 2017 年发布历史记录。

| 发行版本 | 版本 | 发布日期 |
|-----|-----|-----|
| [GA](#GA) | 14.0.1000.169 | 10-2017 |
| [RC2](#RC2) | 14.0.900.75 | 8-2017 |
| [RC1](#RC1) | 14.0.800.90 | 7-2017 |
| CTP 2.1 | 14.0.600.250 | 2017-5 |
| CTP 2.0 | 14.0.500.272 | 2017-4 |
| CTP 1.4 | 14.0.405.198 | 2017-3 |
| CTP 1.3 | 14.0.304.138 | 2017-2 |
| CTP 1.2 | 14.0.200.24 | 2017-1 |
| CTP 1.1 | 14.0.100.187 | 2016-12 |
| CTP 1.0 | 14.0.1.246 | 2016-11 |

## <a id="GA"></a>GA (自 2017 年 10 月)

这是 SQL Server 2017 常规可用性 (GA) 版本。 对于此版本的 SQL Server 引擎版本是 14.0.1000.169。

### <a name="supported-platforms"></a>支持的平台

| 平台 | 文件系统 | 安装指南 |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 或 7.4 工作站、 服务器和桌面 | XFS 或 EXT4 | [安装指南](quickstart-install-connect-red-hat.md) | 
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
| Red Hat RPM 包 | 14.0.1000.169-2 | [引擎 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[SSIS 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| SLES RPM 包 | 14.0.1000.169-2 | [mssql server 引擎 RPM 程序包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[高可用性 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[全文搜索 RPM 包](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[SQL Server 代理 RPM 包](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Ubuntu 16.04 Debian 包 | 14.0.1000.169-2 | [引擎 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[高可用性 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[全文搜索 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[SQL Server 代理 Debian 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[SSIS 包](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

### <a name="supported-client-tools"></a>支持的客户端工具

| 工具 | 最低版本 |
|-----|-----|
| [适用于 Windows 的 SQL Server Management Studio (SSMS)](https://go.microsoft.com/fwlink/?linkid=847722) | 17.0 |
| [SQL Server Data Tools for Visual Studio](https://go.microsoft.com/fwlink/?linkid=846626) | 17.0 |
| [Visual Studio Code](https://code.visualstudio.com)与[mssql 扩展](https://aka.ms/mssql-marketplace) | 最新 |

### <a name="Unsupported"></a>不支持的功能和服务

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
| &nbsp; | 对于链接服务器的 AD 身份验证 | 
| &nbsp; | AD 认证为可用性组 （承载个可用性组） | 
| **服务** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

### <a name="known-issues"></a>已知问题

以下部分介绍在 Linux 上的 SQL Server 2017 生成正式版 (GA) 推出的已知的问题。

#### <a name="general"></a>常规

- 只能从 CTP 2.1 或更高版本支持升级到 GA 版本的 SQL Server 自 2017 年。 

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

      ```bash
      sudo systemctl restart mssql-server
      ```

- 使用内存中 OLTP 的 Windows 上的 SQL Server 2014 数据库无法还原在 Linux 上的 SQL Server 2017 上。 若要还原使用内存中 OLTP 的 SQL Server 2014 数据库，首先将数据库升级到 SQL Server 2016 或 Windows 上的 SQL Server 2017 之前将其移动到 SQL Server 在 Linux 上通过备份/还原或分离/附加。

- 用户权限**ADMINISTER BULK OPERATIONS**不支持在 Linux 上这次。

#### <a name="networking"></a>网络

如果满足以下条件，涉及从 sqlservr 进程，如链接的服务器或可用性组的出站 TCP 连接的功能可能不起作用：

1. 目标服务器指定为主机名而不是 IP 地址。

1. 源实例已在内核中禁用 IPv6。 若要验证你的系统是否有在内核中启用了 IPv6，必须传递所有以下测试：

   - `cat /proc/cmdline`将打印当前内核启动命令行。 输出不能包含`ipv6.disable=1`。
   - / 进程/sys/网络/ipv6/目录必须存在。
   - C 程序中调用`socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)`应成功-syscall 必须返回 fd ！ =-1 并不会因 EAFNOSUPPORT 失败。

具体错误取决于该功能。 对于链接服务器，这种情况登录超时错误。 对于可用性组， `ALTER AVAILABILITY GROUP JOIN` DDL 辅助副本上的将在 5 分钟下载配置超时错误后失败。

若要解决此问题，请执行以下操作：

1. 使用而不是主机名 Ip 指定 TCP 连接的目标。

1. 通过删除启用在内核中的 IPv6`ipv6.disable=1`从启动命令行。 若要执行此操作的方式取决于 Linux 分发和引导加载程序，如 grub。 如果你确实想要禁用的 IPv6，你仍然可以禁用它通过设置`net.ipv6.conf.all.disable_ipv6 = 1`中`sysctl`配置 (例如`/etc/sysctl.conf`)。 这仍将防止系统的网络适配器 IPv6 地址，但允许 sqlservr 功能工作。

#### <a name="network-file-system-nfs"></a>网络文件系统 (NFS)
如果你使用**网络文件系统 (NFS)**在生产中的远程共享，请注意以下支持要求：

- 使用 NFS 版本**4.2 或更高版本**。 NFS 的较旧版本不支持所需的功能，如 fallocate 和稀疏文件创建，普遍适用于现代文件系统。
- 仅查找**/var/opt/mssql**上 NFS 装入的目录。 其他文件，如 SQL Server 系统二进制文件，不支持。
- 确保安装对远程共享时，NFS 客户端，使用 nolock 选项。

#### <a name="localization"></a>本地化

- 如果你的区域设置不是在安装过程英语 (en_us)，则必须使用 utf-8 编码在 bash 会话/终端。 如果你使用 ASCII 编码，可能会看到如下错误：

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   如果你不能使用 utf-8 编码，运行安装程序使用 MSSQL_LCID 环境变量来指定语言选择。

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- 如果运行 mssql conf 安装程序，并执行 SQL Server，不正确的非英语安装扩展字符将显示在本地化文本，"配置 SQL Server …"之后。 或者，对于非拉丁基于安装，可能是缺少句子完全。 缺少句子应显示以下的本地化的字符串:"已成功处理的授权 PID。  新的版本是 [<Name>版本]"。 此字符串输出信息仅用于，和下一步的 SQL Server 累积更新将解决此问题为所有语言。 这不会影响 SQL server 安装以任何方式成功。 

#### <a name="full-text-search"></a>全文搜索

- 并非所有筛选器是此版本，包括 Office 文档的筛选器提供的。 有关受支持的筛选器的列表，请参阅[安装 Linux 上 SQL Server 全文搜索](sql-server-linux-setup-full-text-search.md#filters)。

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- **Mssql 服务器是**包在此版本中不支持在 SUSE 上。 当前支持在 Ubuntu 上和 Red Hat Enterprise Linux (RHEL) 上。

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

有关内置 SSIS 组件当前不支持，或支持有限制的列表，请参阅[提取、 转换和加载数据使用 SSIS 的 Linux 上](sql-server-linux-migrate-ssis.md#components)。

有关在 Linux 上的 SSIS 的详细信息，请参阅以下文章：
-   [博客文章宣布推出适用于 Linux 的 SSIS 支持](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。
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
   
      ```bash
      sudo systemctl restart mssql-server
      ```

- 使用内存中 OLTP 的 Windows 上的 SQL Server 2014 数据库无法还原在 Linux 上的 SQL Server 2017 上。 若要还原使用内存中 OLTP 的 SQL Server 2014 数据库，首先将数据库升级到 SQL Server 2016 或 Windows 上的 SQL Server 2017 之前将其移动到 SQL Server 在 Linux 上通过备份/还原或分离/附加。

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
| &nbsp; | 机器学习服务 |
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

#### <a name="availability-group"></a>可用性组 (availability group)

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

