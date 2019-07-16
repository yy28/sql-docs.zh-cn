---
title: 对 Linux 上的 SQL Server 进行故障排除
description: 提供有关在 Linux 上使用 SQL Server 故障排除提示。
author: VanMSFT
ms.author: vanto
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: 6ff5c1c5944e1313d6c95cd35be288ad4d2154c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032216"
---
# <a name="troubleshoot-sql-server-on-linux"></a>对 Linux 上的 SQL Server 进行故障排除

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文档介绍如何对 Linux 上或 Docker 容器中运行的 Microsoft SQL Server 进行故障排除。 故障排除时在 Linux 上的 SQL Server，请记住要检查的支持的功能和已知的限制[SQL Server 的 Linux 发行说明](sql-server-linux-release-notes.md)。

> [!TIP]
> 有关常见问题的解答，请参阅[SQL Server Linux 常见问题](sql-server-linux-faq.md)。

## <a id="connection"></a> 排除连接故障
如果在连接到 Linux SQL Server 时存在问题，可以检查以下几点。

- 如果您不能使用本地连接**localhost**，请尝试改用 IP 地址 127.0.0.1。 可能的**localhost**未正确映射到此地址。

- 验证可从客户端计算机访问的服务器名称或 IP 地址。

   > [!TIP]
   > 若要查找 Ubuntu 计算机的 IP 地址，可运行 ifconfig 命令，如以下示例所示：
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > 对于 Red Hat，可使用 ip addr，如以下示例所示：
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > 但如果是 Azure VM ，此技术则不适用。 适用于 Azure Vm[在 Azure 门户中查找 VM 的公共 IP](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect)。

- 如果适用，请检查已打开防火墙上的 SQL Server 端口 （默认值为 1433年）。

- 对于 Azure Vm，检查是否有[的默认 SQL Server 端口的网络安全组规则](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote)。

- 验证用户名和密码是否存在任何拼写错误、多余的空格或错误的大小写。

- 尝试显式设置如下例所示的服务器名称的协议和端口号： **servername，1433年**。

- 网络连接问题也会导致连接错误和超时。 验证连接信息和网络连接后，请再次尝试连接。

## <a name="manage-the-sql-server-service"></a>管理 SQL Server 服务

以下部分说明如何启动、停止、重启 SQL Server 服务并检查其状态。 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>管理 mssql server 服务在 Red Hat Enterprise Linux (RHEL) 和 Ubuntu 

检查 SQL Server 服务使用此命令的状态：

   ```bash
   sudo systemctl status mssql-server
   ```

可根据需要使用以下命令停止、启动或重启 SQL Server 服务：

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>管理 mssql Docker 容器的执行

可以通过运行以下命令获取最新创建的 SQL Server Docker 容器的状态和容器 ID (ID 位于**容器 ID**列):

   ```bash
   sudo docker ps -l
   ```
   
可根据需要使用以下命令停止或重启 SQL Server 服务：
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> 有关 Docker 的更多疑难解答提示，请参阅[故障排除 SQL Server Docker 容器](sql-server-linux-configure-docker.md#troubleshooting)。

## <a name="access-the-log-files"></a>访问日志文件
   
SQL Server 引擎在 Linux 和 Docker 安装的 /var/opt/mssql/log/errorlog 文件中进行记录。 您需要在超级用户模式下，若要浏览此目录。

安装程序在此处记录: / var/opt/mssql/安装程序-< representing time of 时间戳 > 您可以浏览错误日志文件使用任何 utf-16 兼容工具如 vim 或 cat 如下所示： 

   ```bash
   sudo cat errorlog
   ```

如果您愿意，您可以还将文件转换为 UTF-8，读取它们与详细或 less 使用以下命令：
   
   ```bash
   sudo iconv -f UTF-16LE -t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>扩展事件

可通过 SQL 命令查询扩展事件。  可以找到有关扩展事件的详细信息[此处](https://technet.microsoft.com/library/bb630282.aspx):

## <a name="crash-dumps"></a>故障转储 

在 Linux 中查看日志目录中的转储。 在 /var/opt/mssql/log 目录下查看 Linux Core 转储（扩展名为 .tar.gz2）或 SQL 小型转储（扩展名为 .mdmp）

对于 Core 转储 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

对于 SQL 转储 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>最小配置中或在单用户模式下启动 SQL Server

### <a name="start-sql-server-in-minimal-configuration-mode"></a>在最小配置模式下启动 SQL Server
在配置值的设置（例如，过度分配内存）妨碍服务器启动时，这非常有用。
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>在单用户模式下启动 SQL Server
在某些情况下，可能需要使用启动选项-m 在单用户模式下启动 SQL Server 的实例。 例如，您可能要更改服务器配置选项或恢复已破坏的 master 数据库或其他系统数据库。 例如，你可能想要更改服务器配置选项或恢复已损坏的主数据库或其他系统数据库   

在单用户模式下启动 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

在使用 SQLCMD 的单用户模式下启动 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  使用“mssql”用户启动 Linux 上的 SQL Server 以防止将来的启动问题。 例如，“sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]” 

如果意外地将 SQL Server 开始另一个用户，您必须将 SQL Server 数据库文件的所有权更改回之前使用 systemd 启动 SQL Server 的 mssql 用户。 例如，若要更改为 mssql 用户 /var/opt/mssql 下的所有数据库文件的所有权，请运行以下命令

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>重新生成系统数据库
作为最后的手段，您可以选择重新生成 master 和 model 数据库返回到默认版本。

> [!WARNING]
> 这些步骤将**删除所有 SQL Server 系统数据**已配置 ！ 这包括用户数据库 （但不是用户数据库本身） 有关的信息。 它也会删除存储在系统数据库，包括以下其他信息： 主要密钥信息，在 master、 SA 登录名密码、 从 msdb 与作业相关的信息、 msdb 和 sp_configure 选项从 DB 邮件信息中加载任何证书。 如果了解影响仅使用 ！

1. 停止 SQL Server。

   ```bash
   sudo systemctl stop mssql-server
   ```

1. 运行**sqlservr**与**强制安装程序**参数。 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > 请参阅上面的警告 ！ 此外，还必须运行此方法作为**mssql**用户，如下所示。

1. 你将看到消息"恢复已完成"后，按 CTRL + C。 这将关闭 SQL Server

1. 重新配置 SA 密码。

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. 启动 SQL Server 和重新配置服务器。 这包括还原或重新附加任何用户数据库。

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>提高性能

有许多因素会影响性能，包括数据库设计、 硬件和工作负荷需求。 如果想要提高性能，首先查看在文章中，最佳做法[的性能最佳实践和 Linux 上的 SQL Server 配置准则](sql-server-linux-performance-best-practices.md)。 然后将探讨一些故障排除性能问题的可用工具。

- [查询存储](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [系统动态管理视图 (Dmv)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [SQL Server Management Studio 中的性能仪表板](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>常见问题

1. 无法连接到远程 SQL Server 实例。

   请参阅本文中，故障排除部分[连接到 Linux 上的 SQL Server](#connection)。

2. 错误：主机名必须是 15 个字符或更少。

   这是一个已知问题，在尝试安装 SQL Server Debian 包的计算机名超过 15 个字符时则会出现此问题。 除了更改计算机名外，目前尚无其他的解决方法。 可以编辑主机名文件并重启计算机以更改此名称。 以下[网站指南](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)详细说明了此。

3. 重置系统管理 (SA) 密码。

   如果您忘记了系统管理员 (SA) 密码，或者需要重置某些其他原因，请执行以下步骤。

   > [!NOTE]
   > 以下步骤暂时停止 SQL Server 服务。

   登录到主机终端，运行以下命令并按照提示重置 SA 密码：

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 在密码中使用特殊字符。

   如果在 SQL Server 登录密码中使用某些字符，可能需要在 Linux 命令，在终端中使用它们时使用反斜杠转义。 例如，您必须转义美元符号 （$） 只要您使用终端命令 /shell 脚本中：

   无效：

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   有效：

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   资源：[特殊字符](https://tldp.org/LDP/abs/html/special-chars.html)
   [转义](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
