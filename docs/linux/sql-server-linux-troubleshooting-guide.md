---
title: "解决在 Linux 上的 SQL Server |Microsoft 文档"
description: "提供有关在 Linux 上使用 SQL Server 2017 故障排除提示。"
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 05/08/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.workload: On Demand
ms.openlocfilehash: 74d1111cab0b0e59ff13644e86ed33323a0185dc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshoot-sql-server-on-linux"></a>对 Linux 上的 SQL Server 进行故障排除

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本文档介绍如何对 Linux 上或 Docker 容器中运行的 Microsoft SQL Server 进行故障排除。 故障排除在 Linux 上的 SQL Server，请记得要检查的支持的功能和中的已知的限制[Linux 发行说明上的 SQL Server](sql-server-linux-release-notes.md)。

## <a id="connection"></a>解决连接失败
如果在连接到 Linux SQL Server 时存在问题，可以检查以下几点。 

- 验证可从客户端计算机的服务器名称或 IP 地址。

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
   > 但如果是 Azure VM ，此技术则不适用。 对于 Azure Vm， [VM 在 Azure 门户中找到的公共 IP](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect)。

- 如果适用，请检查你已打开防火墙上的 SQL Server 端口 （默认值为 1433年）。

- 对于 Azure Vm，请检查您有[的默认 SQL Server 端口的网络安全组规则](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote)。

- 验证用户名和密码是否存在任何拼写错误、多余的空格或错误的大小写。

- 尝试显式设置如下所示的服务器名称的协议和端口号： **tcp:servername，1433年**。

- 连接错误和超时，也会导致网络连接问题。 验证连接信息和网络连接后，请再次尝试连接。

## <a name="manage-the-sql-server-service"></a>管理 SQL Server 服务

以下部分说明如何启动、停止、重启 SQL Server 服务并检查其状态。 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>管理中 Red Hat Enterprise Linux (RHEL) 和 Ubuntu 的 mssql server 服务 

检查 SQL Server 服务使用此命令的状态的状态：

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

通过运行以下命令，可以获得最新创建的 SQL Server Docker 容器的状态和容器 ID（ID 位于“CONTAINER ID”列下）：

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
   
SQL Server 引擎在 Linux 和 Docker 安装的 /var/opt/mssql/log/errorlog 文件中进行记录。 需要启用“超级用户”模式才能浏览此目录。

安装程序在此处记录：/var/opt/mssql/setup-< time stamp representing time of install>。可使用任何 UTF-16 兼容工具（如“vim”或“cat”）浏览错误日志文件，如下所示： 

   ```bash
   sudo cat errorlog
   ```

如果愿意，还可将文件转换为 UTF-8，以使用以下命令通过“more”或“less”读取它们：
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>扩展事件

可通过 SQL 命令查询扩展事件。  可以找到有关扩展事件的更多信息[此处](https://technet.microsoft.com/en-us/library/bb630282.aspx):

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
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>在最小配置中或在单用户模式下启动 SQL Server

### <a name="start-sql-server-in-minimal-configuration-mode"></a>在最小配置模式下启动 SQL Server
在配置值的设置（例如，过度分配内存）妨碍服务器启动时，这非常有用。
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>在单用户模式下启动 SQL Server
在某些情况下，你可能需要使用启动选项-m 在单用户模式下启动 SQL Server 的实例。 例如，您可能要更改服务器配置选项或恢复已破坏的 master 数据库或其他系统数据库。 例如，你可能想要更改服务器配置选项或恢复已损坏的主数据库或其他系统数据库   

在单用户模式下启动 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

在使用 SQLCMD 单用户模式下启动 SQL Server
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  在 Linux 上的 SQL Server 启动与"mssql"的用户，以防止将来启动问题。 示例"sudo-u mssql /opt/mssql/bin/sqlservr [启动选项]" 

如果你意外已经与另一个用户启动 SQL Server，你将需要改回为之前从 SQL Server 开始 systemd mssql 用户的 SQL Server 数据库文件的所有权。 例如，若要将 /var/opt/mssql 下的所有数据库文件的所有权更改为 mssql 的用户，请运行以下命令

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="common-issues"></a>常见的问题

1. 无法连接到远程 SQL Server 实例。

   请参阅疑难解答部分的主题，[连接到 Linux 上的 SQL Server](#connection)。

2. 错误：主机名称必须不超过 15 个字符。

   这是一个已知问题，在尝试安装 SQL Server Debian 包的计算机名超过 15 个字符时则会出现此问题。 除了更改计算机名外，目前尚无其他的解决方法。 可以编辑主机名文件并重启计算机以更改此名称。 以下[网站指南](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/)这解决方案详细说明。

3. 重置系统管理 (SA) 密码。

   如果忘了系统管理员 (SA) 密码，或出于其他原因需要重置密码，请遵循以下步骤。

   > [!NOTE]
   > 执行以下步骤将暂时停止 SQL Server 服务。

   登录到主机终端，运行以下命令并按照提示重置 SA 密码：

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. 在密码中使用特殊字符。

   如果在 SQL Server 登录密码中使用某些字符，则在 Linux 终端中使用这些字符时可能需要对它们进行转义。 每次在终端命令/Shell 脚本中使用 $ 时，需使用反斜杠字符对它进行转义：

   无效：

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   有效：

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   资源：[特殊字符](http://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](http://tldp.org/LDP/abs/html/escapingsection.html)

## <a name="support"></a>支持

可以通过社区获取支持，并且由工程团队核查。 有关特定问题，请参阅以下资源：

- [DBA 堆栈 Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)： 提问数据库管理
- [堆栈溢出](http://stackoverflow.com/questions/tagged/sql-server)： 提出开发问题
- [MSDN 论坛](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)： 询问技术问题
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)： 报告 bug 和请求功能
- [Reddit](https://www.reddit.com/r/SQLServer/)： 讨论 SQL Server
